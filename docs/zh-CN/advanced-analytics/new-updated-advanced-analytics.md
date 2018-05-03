---
title: 更新-为 SQL Server 文档高级分析 |Microsoft 文档
description: 显示更新内容的最近更改中的文档，为 Microsoft SQL server 的高级分析的代码的段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 04/28/2018
ms.openlocfilehash: bbce32579b54647e167c25d2708a80027ae0e678
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新的和最近的更新： SQL Server 的高级分析



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **2018年-02-03** &nbsp;到&nbsp; **2018年-04-28**
- *主题区域：* &nbsp; **for SQL Server 的高级分析**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


1. [安装 SQL Server 自 2017 年 1 机器学习在 Windows 上的服务 （数据库）](install/sql-machine-learning-services-windows-install.md)
2. [安装 SQL Server 自 2017 年 1 机器学习 Windows 上的服务器 （独立）](install/sql-machine-learning-standalone-windows-install.md)
3. [从命令行安装 SQL Server 计算机学习组件](install/sql-ml-component-commandline-install.md)
4. [安装 SQL Server 机器学习没有 internet 访问权限的组件](install/sql-ml-component-install-without-internet-access.md)
5. [安装 SQL Server 2016 R Services （数据库）](install/sql-r-services-windows-install.md)
6. [安装 SQL Server 2016 R Server （独立）](install/sql-r-standalone-windows-install.md)
7. [设置 Python 客户端工具，用于 SQL Server 机器学习](python/setup-python-client-tools-sql.md)
8. [使用在 SQL 中的 Python 模型进行定型集和评分](tutorials/train-score-using-python-in-tsql.md)
9. [将 Python 代码包装在存储过程](tutorials/wrap-python-in-tsql-stored-procedure.md)
10. [什么是 SQL Server 机器学习服务？](what-is-sql-server-machine-learning.md)
11. [用于监视 PREDICT 语句的扩展事件](xe-event-predict-tsql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [查看 R 或在 SQL Server 上安装 Python 包](#TitleNum_1)
2. [安装预先训练的机器学习模型上 SQL Server](#TitleNum_2)
3. [设置 SQL Server 上的 R 开发数据科学客户端](#TitleNum_3)
4. [SQL Server 计算机学习和 R Services （数据库）](#TitleNum_4)
5. [运行 Python 使用 T-SQL](#TitleNum_5)
6. [使用与 revoscalepy Python 创建模型](#TitleNum_6)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-viewing-r-or-python-packages-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>1.&nbsp; [查看 R 或在 SQL Server 上安装 Python 包](r/determine-which-packages-are-installed-on-sql-server.md)

*更新时间： 2018年-04-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 208.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f ec6859ac91b27539dc36f21aec82c99937c0187a  (PR=5610  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f1f96a990644c0d6cfa5a1d88ccee959cab6c2b2) -->



**Python**


此示例返回的 Python 中包含的文件夹列表`sys.path`变量。 该列表包括当前目录和标准库路径。

```
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**结果**

```
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

有关变量的详细信息`sys.path`以及如何使用它来设置的模块的解释程序的搜索路径，请参阅[Python 文档](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-install-pre-trained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>2.&nbsp; [安装预先训练的机器学习模型上 SQL Server](r/install-pretrained-models-sql-server.md)

*更新时间： 2018年-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 140.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 aa03623d819750d4919feb7910b07ec1875bb509 7382228fa68b04b500a5fde73c29995e12aa20ac  (PR=5504  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



1. 启动单独的基于 Windows 的安装程序或者[R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)或[机器学习服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

2. 选择你想要更新，然后选择的语言**Pre-trained 模型**选项。

    > [!TIP]
    > 如果你以前运行安装程序来更新 R Server （独立），并只是想要添加预先训练的模型，保留所有以前选择**原样**，然后选择刚预 **-定型模型**选项. **不这样做**取消选择任何以前选择的选项; 如果这样做，则安装程序中删除组件。

    我们建议你接受模型位置的默认设置。

3. 单击 **“继续”**。

4. 接受所有其他提示，包括许可协议。

安装完成后，你必须执行一些附加步骤以注册预先训练的模型。

1. 打开 Windows 命令提示符**以管理员身份**。

2. R server （独立），还包含 Microsoft R 安装程序，导航到安装程序启动文件夹。

3. 运行`RSetup.exe`并指示要安装的组件、 版本和包含模型源文件，使用此语法的文件夹：

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    版本参数支持以下值：



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-set-up-a-data-science-client-for-r-development-on-sql-serverrset-up-a-data-science-clientmd"></a>3.&nbsp; [设置 SQL Server 上的 R 开发数据科学客户端](r/set-up-a-data-science-client.md)

*更新时间： 2018年-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 39.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0583f8febcedc5dc2e14ca1a8073ca204ca37987 3d50ad8f35f2985944741a9b2211a461df2c13e4  (PR=5504  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



**R 工具**


当与 SQL Server 安装 R 时，可以使用任何安装的相同 R 工具**基**R，如 RGui、 Rterm，等的安装。 因此从技术上讲，你具有所需开发和测试 R 代码的所有工具。

以下标准 R 工具都将纳入*基本安装*，因此默认情况下安装。

+ **RTerm**： 用于运行 R 脚本的命令行终端

+ **RGui.exe**：适用于 R 的简单交互式编辑器。RGui.exe 和 RTerm 的命令行参数相同。

+ **RScript**：用于以批处理模式运行 R 脚本的命令行工具。

若要找到这些工具，确定设置 SQL Server 或独立机器学习功能一起安装的 R 库。 例如，在默认安装中，R 工具位于以下文件夹：

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server 独立： `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 自 2017 年 1 机器学习服务： `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ 机器学习 Server （独立）： `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

如果你需要使用 R 工具的帮助，只需打开**RGui**，单击**帮助**，然后选择其中一个选项

**Microsoft R Client**


Microsoft R 客户端是一个免费下载，使你可以访问的开发使用 RevoScaleR 包。 通过安装 R 客户端，你可以创建可以在所有受支持的计算上下文，包括 SQL Server 数据库中分析和分布式 R 计算 Hadoop、 Spark 中或使用机器学习服务器的 Linux 上运行的 R 解决方案。

如果你已安装不同的 R 开发环境，如 RStudio，一定要重新配置要使用的库和可执行文件由 Microsoft R 客户端提供的环境。 通过这样你可以使用 RevoScaleR 包的所有功能尽管性能将受到限制。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sql-server-machine-learning-and-r-services-in-databasersql-server-r-servicesmd"></a>4.&nbsp; [SQL Server 计算机学习和 R Services （数据库）](r/sql-server-r-services.md)

*更新时间： 2018年-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 83.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b1a95a7f6d391a518762eb271e8ea7e0d684d403 7fbfabf62917e03e2bcb99d297e1c9d0f0604440  (PR=5504  ,  Filename=sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



选择该任务的最佳语言。 使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的数据操作，利用 *{包含的内容-会-此处}* 以获得最大性能。 对列进行快速计算时，可使用内存数据库引擎。

**步骤 4： 优化你的解决方案**


在该模型已准备好企业数据上的缩放，数据科研人员通常与 DBA 或 SQL 开发人员可以如优化进程方式工作：

+ 特征工程
+ 数据引入和数据转换
+ 计分

通常，使用 R 的数据科研人员在性能和伸缩性两方面都会遇到问题，尤其是在使用大型数据集时。 因为通用运行时实现是单线程的，只能适应可装入本地计算机上可用内存的数据集。 与 SQl Server 机器学习服务集成可以提供多种功能，带来更好的性能，并处理更多的数据：

+ **RevoScaleR**： 此 R 包中包含的一些最常用 R 函数，重新设计，以提供并行度和缩放实现。 该包还包含函数来进一步提升性能和可扩展性，通过将推送到计算 *{包含的内容-会-此处}* 计算机，它通常具有大得多的内存和计算能力。

+ **revoscalepy**。 此 Python 库，位于 SQL Server 自 2017 年，例如远程计算上下文，RevoScaleR，在实现最常用的函数和许多支持的算法分布式处理。

**资源**

+ [性能案例研究]
+ [R 和数据优化]

**步骤 5： 部署和使用**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-run-python-using-t-sqltutorialsrun-python-using-t-sqlmd"></a>5.&nbsp; [运行 Python 使用 T-SQL](tutorials/run-python-using-t-sql.md)

*更新时间： 2018年-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 306.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bde8c6476df259d225847c08224cefd02f3529d5 cad56997abe7928b588ac4a0302384c5edc1ede5  (PR=5497  ,  Filename=run-python-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



2. 请注意索引值不是输出，即使你使用索引从 data.frame 获取特定值。

    **结果**

    |ResultValue|
    |------|
    |0.5|
    |2|

**输出值插入 data.frame 使用索引**


让我们了解我们包含简单的数学运算结果的两个序列时，转换为 data.frame 的工作原理。 第一个已生成的 Python 的顺序值的索引。 第二个使用任意字符串值的索引。

1. 此示例使用整数索引序列中获取一个值。

```
    EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
```

请记住从 0 开始的自动生成的索引。 尝试使用范围索引值外，请参阅会发生什么情况。

2. 现在让我们从其他具有字符串索引的数据帧中获取单个值。

```
    EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
```

**结果**

|ResultValue|
|------|
|0.5|

如果你尝试使用数字索引这一系列从获取一个值，则会出现错误。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>6.&nbsp; [使用与 revoscalepy Python 创建模型](tutorials/use-python-revoscalepy-to-create-model.md)

*更新时间： 2018年-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_5))

<!-- Source markdown line 22.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5b642b391ca571412c30c8470875d3d4d3c57246 bd83387eb8a1076a1396bbd48dca12872843aa2f  (PR=5497  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



如果你安装 SQL Server 自 2017 年的预发行版本，则应更新到至少的 RTM 版本。 更高版本的服务版本不断扩展和改进 Python 功能。 本教程中的某些功能可能无法在早期的预发行版本。

+ 此示例使用预定义的 Python 环境中，名为`PYTEST_SQL_SERVER`。 配置环境以包含**revoscalepy**和其他所需的库。

    如果你没有配置为运行 Python 环境，你必须单独执行此操作。 如何创建或修改 Python 环境的讨论不在本教程的范围之内。 有关如何设置包含正确的库的 Python 客户端的详细信息，请参阅[安装 Python 客户端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)和[到工具的链接 Python](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。

**远程计算上下文和 revoscalepy**


此示例演示如何在远程创建 Python 模型的过程_计算上下文_，该对话框允许您从客户端，但选择远程环境，如 SQL Server、 Spark 中或计算机学习服务器，其中实际执行的操作。 使用计算上下文，可以更轻松地编写代码一次，并将其部署到任何受支持的环境。

若要在 SQL Server 中执行 Python 代码，需要**revoscalepy**包。 这是由 Microsoft，类似于提供特殊的 Python 包**RevoScaleR** R 语言包。 **Revoscalepy**包支持创建计算上下文，并提供用于在本地工作站和远程服务器之间传递数据和模型的基础结构。 **Revoscalepy**函数的支持的数据库中的代码将执行[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (11 + 6): &nbsp; &nbsp; **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (18 + 0): &nbsp; &nbsp; **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (218 + 14):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (14 + 0): &nbsp; &nbsp; **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (3 + 2): &nbsp; &nbsp; **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (3 + 3): &nbsp; &nbsp; **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (7 + 10): &nbsp; &nbsp; **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 2): &nbsp; &nbsp; **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 3): &nbsp; &nbsp; **SQL 操作 Studio**文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): &nbsp; &nbsp; **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (1 + 1): &nbsp; &nbsp; **SQL 的工具**文档](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章

- [新 + 更新 (0 + 0): **SQL 的分析平台系统**文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **sql 的 ODBC （开放式数据库连接）**文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**适用于 SQL PowerShell**文档](../powershell/new-updated-powershell.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../samples/new-updated-samples.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)** 文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)

