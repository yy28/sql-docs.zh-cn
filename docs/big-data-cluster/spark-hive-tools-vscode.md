---
title: 针对 SQL Server 大数据群集上的 VS Code 运行具有 Spark 的 spark 作业 & Hive 工具
titleSuffix: SQL Server big data clusters
description: 将 spark 作业提交到 SQL Server 大数据群集上的 Spark & Hive 工具来 Visual Studio Code。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425977"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>在 Visual Studio Code 中 SQL Server 大数据群集上提交 Spark 作业

了解如何使用 Spark & Hive 工具来 Visual Studio Code 为 Apache Spark 创建和提交 PySpark 脚本。首先, 我们将介绍如何在 Visual Studio Code 中安装 Spark & Hive 工具, 然后我们将逐步介绍如何将作业提交到 Spark。  

可以在 Visual Studio Code 支持的平台 (包括 Windows、Linux 和 macOS) 上安装 Spark & Hive 工具。 下面你会发现不同平台的先决条件。


## <a name="prerequisites"></a>系统必备

若要完成本文中的步骤, 需要以下各项:

- SQL Server 大数据群集。 请参阅[SQL Server 大数据群集](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)。
- [Visual Studio Code](https://code.visualstudio.com/)。
- [Mono](https://www.mono-project.com/docs/getting-started/install/)。 只有 Linux 和 macOS 需要 Mono。
- [为 Visual Studio Code 设置 PySpark 交互式环境](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment)。
- 名为**HDexample**的本地目录。  本文使用**C:\HD\HDexample**。

## <a name="install-spark--hive-tools"></a>安装 Spark & Hive 工具

完成先决条件后, 可以为 Visual Studio Code 安装 Spark & Hive 工具。  完成以下步骤以安装 Spark & Hive 工具:

1. 打开 Visual Studio Code。

2. 从菜单栏中, 导航到 "**查看** > **扩展**"。

3. 在搜索框中, 输入**Spark & Hive**。

4. 从搜索结果中选择 " **Spark & Hive 工具**", 然后选择 "**安装**"。  

   ![安装扩展](./media/spark-hive-tools-vscode/extension.png)

5. 需要时重新加载。

## <a name="open-work-folder"></a>打开工作文件夹

完成以下步骤以打开工作文件夹, 然后在 Visual Studio Code 中创建文件:

1. 从菜单栏中, 导航到 "**文件** > " "**打开文件夹 ...** "C:\HD\HDexample, 然后选择 "**选择文件夹**" 按钮。   >  文件夹将显示在左侧的**资源管理器**视图中。

2. 在**资源管理器**视图中, 选择 " **HDexample**" 文件夹, 然后选择 "工作文件夹" 旁边的 "**新建文件**" 图标。

   ![新建文件](./media/spark-hive-tools-vscode/new-file.png)

3. 将新文件命名为`.py` (Spark script) 文件扩展名。  此示例使用**HelloWorld.py**。
4. 将以下代码复制并粘贴到脚本文件中:
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>链接 SQL Server 大数据群集

在从 Visual Studio Code 将脚本提交到群集之前, 需要链接 SQL Server 大数据群集。

1. 从菜单栏中, 导航到 "**查看** > **命令面板 ...** ", 然后**输入 Spark/Hive:链接群集”。**

   ![链接群集命令](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. 选择链接群集类型**SQL Server 大数据**。

3. 输入 SQL Server 大数据终结点。

4. 输入 SQL Server 大数据群集用户名。

5. 输入用户管理员的密码。

6. 设置群集的显示名称 (可选)。

7. 列出群集, 查看要验证的**输出**视图。

## <a name="list-clusters"></a>列出群集

1. 从菜单栏中, 导航到 "**查看** > **命令面板 ...** ", 然后**输入 Spark/Hive:列出群集**。

2. 查看 "**输出**" 视图。  视图将显示链接的群集。

    ![设置默认群集配置](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>设置默认群集

1. 重新打开[之前](#open-work-folder)创建的文件夹**HDexample** (如果已关闭)。  

2. 选择[之前](#open-work-folder)创建的**HelloWorld.py**文件, 它将在脚本编辑器中打开。

3. 如果尚未链接群集, 请将其链接。

4. 右键单击脚本编辑器, 然后选择**Spark/Hive:设置默认群集**。   

5. 选择一个群集作为当前脚本文件的默认群集。 工具将自动更新配置文件 **。VSCode\settings.json**。 

   ![设置默认群集配置](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>提交交互式 PySpark 查询

可以按照以下步骤提交交互式 PySpark 查询:

1. 重新打开[之前](#open-work-folder)创建的文件夹**HDexample** (如果已关闭)。  

2. 选择[之前](#open-work-folder)创建的**HelloWorld.py**文件, 它将在脚本编辑器中打开。

3. 如果尚未链接群集, 请将其链接。

4. 选择所有代码, 右键单击脚本编辑器, 选择**Spark:PySpark Interactive**以提交查询, 或使用快捷方式**Ctrl + Alt + I**。

   ![pyspark 交互上下文菜单](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. 如果尚未指定默认群集, 请选择该群集。 几分钟后, **Python 交互式**结果将显示在新的选项卡中。这些工具还允许使用上下文菜单提交代码块而非整个脚本文件。 

   ![pyspark 交互 python 交互窗口](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. 输入 **"%% info"** , 然后按**Shift + enter**查看作业信息。 （可选）

   ![查看作业信息](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > 如果在设置中未选中 "**启用 Python 扩展**" (默认设置为选中), 则提交的 pyspark 交互结果将使用旧窗口。
   >
   > ![已禁用 pyspark interactive python 扩展](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>提交 PySpark 批处理作业

1. 重新打开[之前](#open-work-folder)创建的文件夹**HDexample** (如果已关闭)。  

2. 选择[之前](#open-work-folder)创建的**HelloWorld.py**文件, 它将在脚本编辑器中打开。

3. 如果尚未链接群集, 请将其链接。

4. 右键单击脚本编辑器, 然后选择**Spark:PySpark 批处理**, 或使用快捷方式**Ctrl + Alt + H**。 

5. 如果尚未指定默认群集, 请选择该群集。 提交 Python 作业后, 提交日志会显示在 Visual Studio Code 的 "**输出**" 窗口中。 还显示了**SPARK UI url**和**Yarn ui url** 。 你可以在 web 浏览器中打开 URL 以跟踪作业状态。

   ![提交 Python 作业结果](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Apache Livy 配置

支持[Apache Livy](https://livy.incubator.apache.org/)配置, 可将其设置为 **。** 工作空间文件夹中的 VSCode\settings.json。 目前, Livy 配置仅支持 Python 脚本。 更多详细信息, 请参阅[LIVY 自述文件](https://github.com/cloudera/livy/blob/master/README.rst )。

### <a id="triggerlivyconf"></a>**如何触发 Livy 配置**

#### <a name="method-1"></a>方法 1

1. 从菜单栏中, 导航到 "**文件** > " "**首选项** > " "**设置**"。  
2. 在 "**搜索设置**" 文本框中 **, 输入 HDInsight Job Sumission:Livy 会议**  
3. 对于相关的搜索结果, 请选择 "**编辑"。**

#### <a name="method-2"></a>方法 2

提交文件, 请注意`.vscode` , 会自动将文件夹添加到工作文件夹。 可以通过单击`.vscode\settings.json`查找 Livy 配置。

+ 项目设置:

    ![Livy 配置](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>对于 "设置**driverMomory** " 和 " **executorMomry**", 请将值设置为 "单元", 例如1g 或1024m。 

### <a name="supported-livy-configurations"></a>支持的 Livy 配置

#### <a name="post-batches"></a>POST/batches

**请求正文**

| name | description | type |
| :- | :- | :- |
| 文件 | 包含要执行的应用程序的文件 | 路径 (必需) |
| Hadoop.proxyuser.hadoop.hosts | 运行作业时要模拟的用户 | string |
| className | 应用程序 Java/Spark main 类 | string |
| args | 应用程序的命令行参数 | 字符串列表 |
| jar | 此会话中要使用的 jar | 字符串列表 |
| pyFiles | 此会话中要使用的 Python 文件 | 字符串列表 |
| files | 此会话中要使用的文件 | 字符串列表 |
| driverMemory | 要用于驱动程序进程的内存量 | string |
| driverCores | 要用于驱动程序进程的内核数 | INT |
| executorMemory | 每个执行器进程使用的内存量 | string |
| executorCores | 每个执行器要使用的内核数 | INT |
| numExecutors | 为此会话启动的执行器数 | INT |
| 截至 | 此会话中要使用的存档 | 字符串列表 |
| queue | 已提交到的 YARN 队列的名称 | string |
| name | 此会话的名称 | string |
| conf | Spark 配置属性 | Key = val 的映射 |

#### <a name="response-body"></a>响应正文

创建的批处理对象。

| name | description | type |
| :- | :- | :- |
| id | 会话 id | INT |
| appId | 此会话的应用程序 id | String |
| appInfo | 详细的应用程序信息 | Key = val 的映射 |
| 日志 | 日志行 | 字符串列表 |
| state | 批处理状态 | string |

>[!NOTE]
>提交脚本时, 分配的 Livy 配置将显示在输出窗格中。

## <a name="additional-features"></a>其他功能

Spark & Hive for Visual Studio Code 支持以下功能:

- **IntelliSense 自动完成**。 建议弹出关键字、方法、变量等。 不同的图标表示不同类型的对象。

    ![Spark & 用于 Visual Studio Code IntelliSense 对象类型的 Hive 工具](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **IntelliSense 错误标记**。 语言服务会为 Hive 脚本的编辑错误加下划线。     
- **语法突出显示**。 语言服务使用不同的颜色来区分变量、关键字、数据类型、函数等。 

    ![Spark & Hive 工具来 Visual Studio Code 语法突出显示](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>断开群集

1. 从菜单栏中, 导航到 "**查看** > **命令面板 ...** ", 然后输入**Spark/Hive:Unlink a Cluster。**  

2. 选择要取消链接的群集。  

3. 查看**输出**视图以便验证。  

## <a name="next-steps"></a>后续步骤
有关 SQL Server 大数据群集和相关方案的详细信息, 请参阅[SQL Server 大数据群集](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)。
