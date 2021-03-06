---
title: HDInsight 上で Apache Hive とリモート デスクトップを使用する - Azure
description: リモート デスクトップを使用して HDInsight で Hadoop クラスターに接続し、Hive コマンド ライン インターフェイスを使用して Hive クエリを実行する方法について説明します。
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 01/12/2017
ms.author: hrasheed
ROBOTS: NOINDEX
ms.openlocfilehash: 6e0641f2d9427133f951ef63720b4efdac4defe5
ms.sourcegitcommit: c37122644eab1cc739d735077cf971edb6d428fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53409056"
---
# <a name="use-apache-hive-with-apache-hadoop-on-hdinsight-with-remote-desktop"></a>HDInsight 上の Apache Hadoop で、リモート デスクトップを使用して Apache Hive を使用する
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

この記事では、リモート デスクトップを使用して HDInsight クラスターに接続し、Hive コマンド ライン インターフェイス (CLI) を使用して Apache Hive クエリを実行する方法について説明します。

> [!IMPORTANT]  
> リモート デスクトップは、オペレーティング システムとして Windows を使用する HDInsight クラスターでのみ使用できます。 Linux は、バージョン 3.4 以上の HDInsight で使用できる唯一のオペレーティング システムです。 詳細については、[Windows での HDInsight の提供終了](../hdinsight-component-versioning.md#hdinsight-windows-retirement)に関する記事を参照してください。
>
> HDInsight 3.4 以上でのクラスターでのコマンド ラインからの直接的な Hive クエリの実行に関する情報については、[HDInsight と Beeline での Apache Hive の使用](apache-hadoop-use-hive-beeline.md)に関するページを参照してください。

## <a id="prereq"></a>前提条件
この記事の手順を完了するには、次のものが必要です。

* Windows ベースの HDInsight (HDInsight で Hadoop を使用) クラスター
* Windows 10、Window 8、Windows 7 を実行するクライアント コンピューター

## <a id="connect"></a>リモート デスクトップへの接続
「 [RDP を使用した HDInsight クラスターへの接続](../hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)」の手順に従って、HDInsight クラスターのリモート デスクトップを有効にしてからデスクトップに接続します。

## <a id="hive"></a>Hive コマンドの使用
HDInsight クラスターのデスクトップに接続したら、次の手順に従って Hive を使用します。

1. HDInsight デスクトップから、 **Hadoop コマンド ライン**を起動します。
2. 次のコマンドを入力して、Hive CLI を起動します。

        %hive_home%\bin\hive

    CLI が起動すると、Hive CLI プロンプトの `hive>`が表示されます。
3. CLI を使用して次のステートメントを入力し、サンプル データを使用して **log4jLogs** という名前の新しいテーブルを作成します。

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    これらのステートメントは次のアクションを実行します。

   * **DROP TABLE**:テーブルが既存の場合にテーブルとデータ ファイルを削除します。
   * **CREATE EXTERNAL TABLE**:新しい "外部" テーブルを Hive に作成します。 外部テーブルは、Hive にテーブル定義のみを格納し、データは、元の場所に残します。

     > [!NOTE]  
     > 基盤となるデータを外部ソースによって更新する (データの自動アップロード処理など) 場合や別の MapReduce 操作によって更新する場合に、Hive クエリで最新のデータを使用する場合は、外部テーブルを使用する必要があります。
     >
     > 外部テーブルを削除しても、データは削除**されません**。テーブル定義のみが削除されます。
     >
     >
   * **ROW FORMAT**:Hive にデータの形式を示します。 ここでは、各ログのフィールドは、スペースで区切られています。
   * **STORED AS TEXTFILE LOCATION**:Hive に、データの格納先 (example/data ディレクトリ) と、データがテキストとして格納されていることを示します。
   * **SELECT**:**t4** 列の値が **[ERROR]** であるすべての行の数を指定します。 ここでは、この値を含む行が 3 行あるため、 **3** という値が返されています。
   * **INPUT__FILE__NAME LIKE '%.log'** - Hive に .log で終わるファイルのデータのみを返す必要があることを示します。 これにより、検索はデータを含む sample.log ファイルに制限され、定義したスキーマに一致しない他のサンプル データ ファイルのデータを返すことができなくなります。
4. 次のステートメントを使用して、 **errorLogs**という名前の新しい "内部" テーブルを作成します。

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    これらのステートメントは次のアクションを実行します。

   * **CREATE TABLE IF NOT EXISTS**:既存のテーブルが存在しない場合、テーブルを作成します。 **EXTERNAL** キーワードが使用されていないため、これは内部テーブルであり、Hive のデータ ウェアハウスに格納され、Hive によって完全に管理されます。

     > [!NOTE]  
     > **EXTERNAL** テーブルとは異なり、内部デーブルを削除すると、基盤となるデータは削除されます。
     >
     >
   * **STORED AS ORC**:Optimized Row Columnar (ORC) 形式でデータを格納します。 この形式は、Hive にデータを格納するための、非常に効率的で適切な形式です。
   * **INSERT OVERWRITE ...SELECT**:**[ERROR]** を含む **log4jLogs** テーブルの列を選択し、**errorLogs** テーブルにデータを挿入します。

     **errorLogs** テーブルには t4 列に **[ERROR]** を含む列のみが格納されていることを確認するには、次のステートメントを使用して、**errorLogs** 列からすべての列を返します。

       SELECT * from errorLogs;

     3 つのデータ行が返され、各行の t4 列には **[ERROR]** が含まれます。

## <a id="summary"></a>概要
このように、Hive コマンドを使用すると、HDInsight クラスターで簡単に対話的に Hive クエリを実行し、ジョブ ステータスを監視し、出力を取得できます。

## <a id="nextsteps"></a>次のステップ
HDInsight での Hive に関する全般的な情報

* [HDInsight 上の Apache Hadoop で Apache Hive を使用する](hdinsight-use-hive.md)

HDInsight での Hadoop のその他の使用方法に関する情報

* [HDInsight 上の Apache Hadoop で Apache Pig を使用する](hdinsight-use-pig.md)
* [HDInsight 上の Apache Hadoop で MapReduce を使用する](hdinsight-use-mapreduce.md)

Hive で Tez を使用する場合、デバッグ情報については、次のドキュメントを参照してください。

* [Windows ベースの HDInsight で Apache Tez UI を使用して Tez ジョブをデバッグする](../hdinsight-debug-tez-ui.md)
* [Linux ベースの HDInsight で Apache Ambari ビューを使用して Tez ジョブをデバッグする](../hdinsight-debug-ambari-tez-view.md)

[1]:apache-hadoop-visual-studio-tools-get-started.md

[azure-purchase-options]: https://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: https://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: https://azure.microsoft.com/pricing/free-trial/

[apache-tez]: https://tez.apache.org
[apache-hive]: https://hive.apache.org/
[apache-log4j]: https://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: https://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: https://technet.microsoft.com/library/ee692792.aspx
