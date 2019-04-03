---
title: Spark 作业的 Azure 工具包中用于 IntelliJ 群集上运行 SQL Server 大数据
titleSuffix: SQL Server big data clusters
description: 提交用于 IntelliJ 的 Azure 工具包中的 SQL Server 大数据群集上的 Spark 作业。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e48aebbb15b9bd684b2ed3f5d4d314191a55ba42
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860319"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-intellij"></a>提交在 IntelliJ 中的 SQL Server 大数据群集上的 Spark 作业

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 大数据群集的重要方案之一是将提交 Spark 作业的功能。 Spark 作业提交功能，可提交本地 Jar 或上一年度文件与对 SQL Server 大数据群集的引用。 它还可以执行 Jar 或上一年度文件，其中已存在于 HDFS 文件系统中。 

## <a name="prerequisites"></a>先决条件

- SQL Server 大数据群集。
- Oracle Java 开发工具包。 您可以从中进行安装[Oracle 网站](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
- IntelliJ IDEA。 您可以从中进行安装[JetBrains 网站](https://www.jetbrains.com/idea/download/)。
- Azure Toolkit for IntelliJ 扩展。 有关安装说明，请参阅[安装用于 IntelliJ 的 Azure 工具包](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation)。

## <a name="link-sql-server-big-data-cluster"></a>链接 SQL Server 大数据群集
1. 打开 IntelliJ IDEA 工具。

2. 如果使用自签名的证书，禁用从 SSL 证书验证**工具**菜单中，选择**Azure**，**验证 Spark 群集的 SSL 证书**，然后**禁用**。

    ![将 SQL Server 大数据群集链接-禁用 SSL](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. 打开从 Azure 资源管理器**视图**菜单中，选择**工具 Windows**，然后选择**Azure 资源管理器**。
4. 右键单击**SQL Server 大数据群集**，选择**链接 SQL Server 大数据群集**。 输入**服务器**，**用户名**，并**密码**，然后单击**确定**。

    ![将大数据群集的链接对话框](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. 不受信任的服务器证书对话框出现时，单击**接受**。 您可以更高版本管理的证书，请参阅[服务器证书](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html)。

6. 链接的群集将列在下面**SQL Server 大数据群集**。 你可以通过打开 spark 历史记录 UI 和 Yarn UI 来监视 spark 作业，你可能还取消链接，通过右键单击在群集上。

    ![将大数据群集的上下文菜单链接](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-hdinsight-template"></a>从 HDInsight 模板创建 Spark Scala 应用程序

1. 启动 IntelliJ IDEA 并创建一个项目。 在中**新的项目**对话框中，请遵循以下步骤： 

   a. 选择**Azure 的 Spark HDInsight** > **Spark 的示例 (Scala) 项目**。

   b. 在中**生成工具**列表中，选择任一以下命令，根据需要：

      * **Maven**，用于支持 Scala 项目创建向导
      * **SBT**、 用于管理依赖项和生成 Scala 项目

    ![新建项目对话框](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. 选择“**下一步**”。

3. Scala 项目创建向导会自动检测是否已安装了 Scala 插件。 选择“安装”。

   ![Scala 插件检查](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. 若要下载 Scala 插件，请选择**确定**。 按照说明重新启动 IntelliJ。 

   ![Scala 插件安装对话框](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. 在中**新的项目**窗口中，执行以下步骤：  

    ![选择 Spark SDK](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. 输入项目名称和位置。

   b. 在中**项目 SDK**下拉列表中，选择**Java 1.8** Spark 2.x 群集，或选择**Java 1.7**适用于 Spark 1.x 群集。

   c. 在中**Spark 版本**下拉列表中，Scala 项目创建向导集成 Spark SDK 和 Scala SDK 的正确版本。 如果 Spark 群集版本早于 2.0，请选择**Spark 1.x**。 否则，请选择**spark 2.x**。 此示例使用**Spark 2.0.2 (Scala 2.11.8)**。

6. 选择“完成”。

7. Spark 项目会自动为你创建项目。 若要查看该项目，请执行以下步骤操作：

   a. 上**文件**菜单中，选择**项目结构**。

   b. 在中**项目结构**对话框中，选择**项目**若要查看创建的默认项目。 此外可以创建自己的项目，通过选择加号 (**+**)。

      ![在对话框中的项目信息](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>应用程序提交到 SQL Server 大数据群集
链接 SQL Server 大数据群集之后, 可以提交到该应用程序。

1. 设置中配置**运行/调试配置**窗口中，单击 +->**SQL Server 上的 Apache Spark**，选择选项卡**在群集中远程运行**，设置作为参数然后单击确定。

    ![交互式控制台添加配置条目](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![将大数据群集的配置链接](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * 有关**Spark 群集 (仅限 Linux)**，选择你想要运行你的应用程序的群集。

    * 从 IntelliJ 项目中，选择一个项目或从硬盘中选择一个。

    * **主类名**字段：默认值是从所选文件的主类。 可以通过选择省略号更改类 (**...**)，然后选择另一个类。   

    * **作业配置**字段：默认值设置为上面所示的图片。 可以更改值或添加新的键/值的作业提交。 详细信息：  [Apache Livy REST API](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![Spark 提交对话框框作业配置含义](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **命令行参数**字段：可以输入通过空格与主类根据需要拆分的参数值。

    * **引用 Jar**并**引用文件**字段：如果有的话，可以输入的路径以及该被引用的 Jar 文件。 详细信息：  [Apache Spark 配置](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![这意味着 Spark 提交对话框框中 jar 文件](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > 若要上传您的引用 Jar 和引用的文件，请参阅：[如何上传到群集的资源](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **上传路径**:您可以指示 Jar 或 Scala 项目资源提交的存储位置。 有几种受支持的存储类型：**使用 Spark 的交互式会话将上传**和**使用 WebHDFS 要上传**
    
2. 单击**SparkJobRun**提交您的项目与所选分类。 **远程群集中的 Spark 作业**选项卡在底部显示的作业执行进度。 可以通过单击红色按钮停止应用程序。  

    ![链接大数据群集的运行](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Spark 控制台
您可以运行 Spark 本地 Console(Scala) 或运行 Spark Livy 交互式会话 Console(Scala)。

### <a name="spark-local-consolescala"></a>Spark 本地 Console(Scala)
请确保你已经满足 WINUTILS。EXE 必备组件。

1. 从菜单栏中，导航到**运行** > **编辑配置...**.

2. 从**运行/调试配置**窗口中的，在左窗格中，导航到**SQL Server 大数据群集上的 Apache Spark** > **[SQL 上的 Spark] myApp**。

3. 从主窗口中，选择**本地运行**选项卡。

4. 提供以下值，然后选择**确定**:

    |属性 |ReplTest1 |
    |----|----|
    |作业的主类|默认值是从所选文件的主类。 可以通过选择省略号更改类 (**...**)，然后选择另一个类。|
    |环境变量|请确保 HADOOP_HOME 的值正确。|
    |WINUTILS.exe 位置|请确保路径正确无误。|

    ![本地控制台设置配置](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. 从项目中，导航到**myApp** > **src** > **主要** > **scala**  >  **myApp**。  

6. 从菜单栏中，导航到**工具** > **Spark 控制台** > **运行 Spark 本地 Console(Scala)**。

7. 然后可能会显示两个对话框询问你是否想要自动修复依赖项。 如果是这样，选择**自动修复**。

    ![Spark 自动 Fix1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Spark 自动 Fix2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. 在控制台应类似于下面的图片。 在控制台窗口中键入`sc.appName`，然后按 ctrl + Enter。  将显示结果。 可以通过单击红色按钮来终止本地控制台。

    ![本地控制台结果](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Spark Livy 交互式会话 Console(Scala)
IntelliJ 2018.2 和 2018.3 仅支持 Spark Livy 交互式会话 Console(Scala)。

1. 从菜单栏中，导航到**运行** > **编辑配置...**.

2. 从**运行/调试配置**窗口中的，在左窗格中，导航到**SQL Server 大数据群集上的 Apache Spark** > **[SQL 上的 Spark] myApp**。

3. 从主窗口中，选择**在群集中远程运行**选项卡。

4. 提供以下值，然后选择**确定**:

    |属性 |ReplTest1 |
    |----|----|
    |Spark 群集 (仅限 Linux)|选择你想要运行你的应用程序的 SQL Server 大数据群集。|
    |主类名|默认值是从所选文件的主类。 可以通过选择省略号更改类 (**...**)，然后选择另一个类。|

    ![交互式控制台设置配置](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. 从项目中，导航到**myApp** > **src** > **主要** > **scala**  >  **myApp**。  

6. 从菜单栏中，导航到**工具** > **Spark 控制台** > **运行 Spark Livy 交互式会话 Console(Scala)**。

7. 在控制台应类似于下面的图片。 在控制台窗口中键入`sc.appName`，然后按 ctrl + Enter。  将显示结果。 可以通过单击红色按钮来终止本地控制台。

    ![交互式控制台结果](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>将所选内容发送到 Spark 控制台

为方便起见，您可以通过将一些代码发送到本地控制台或 Livy 交互式会话 Console(Scala) 看到的脚本结果。 可以突出显示一些代码放在 Scala 文件，然后右击**将所选内容发送到 Spark 控制台**。 所选的代码将发送到控制台并执行。 在控制台中的代码后，将显示结果。 如果现有，控制台将检查错误。  

   ![将所选内容发送到 Spark 控制台](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>后续步骤
SQL Server 大数据群集和相关的方案的详细信息，请参阅[什么是 SQL Server 2019 大数据群集](big-data-cluster-overview.md)？
