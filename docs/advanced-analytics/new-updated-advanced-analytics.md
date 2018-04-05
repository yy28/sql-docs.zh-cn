---
title: 更新-为 SQL Server 文档高级分析 |Microsoft 文档
description: 显示更新内容的最近更改中的文档，为 Microsoft SQL server 的高级分析的代码的段。
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 02/03/2018
ms.openlocfilehash: dcd40475cb297d480a76f2cb656f8d7ae790f10c
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新的和最近的更新： SQL Server 的高级分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- 更新日期范围：2017-12-03 到 2018-02-03
- *主题区域：* &nbsp; **for SQL Server 的高级分析**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新项目

单击以下链接可跳转到最近添加的新文章。


1. [在 SQL Server 上安装新 Python 包](python/install-additional-python-packages-on-sql-server.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [机器学习服务中的已知的问题](#TitleNum_1)
2. [转换执行数据库中的 R 代码](#TitleNum_2)
3. [确定 SQL 服务器上安装哪些 R 包](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1.&nbsp; [机器学习服务中的已知的问题](known-issues-for-sql-server-machine-learning-services.md)

*更新时间： 2018年-02-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 163.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c6f46adcf795c43f818120b88407a3a89304cb27 c781562605f5cd77f6c43bfe5e89810cb72ceae0  (PR=4789  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=386bfb688843bac7fa4d83dc1cfef94dd19db110) -->



有关可能会影响 R 解决方案的更多已知问题，请参阅[机器学习服务器](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站点。

**在非默认位置中的 SQL Server 上执行 R 脚本时，则拒绝警告**


如果 SQL Server 的实例已安装到非默认位置，如外部`Program Files`文件夹中，当你尝试运行安装包的脚本时引发 ACCESS_DENIED 警告。 例如：

> *In normalizePath(path.expand(path), winslash, mustWork) : path[2]="~ExternalLibraries/R/8/1": Access is denied*

R 函数尝试进行读取的路径，而且如果失败，原因是内置的用户组**SQLRUserGroup**，不具有读取权限。 引发警告不会阻止执行当前的 R 脚本，但警告可能重复发生，每当用户在运行任何其他 R 脚本。

如果在你安装 SQL Server 的默认位置，此错误不会发生，因为所有的 Windows 用户具有读取权限上`Program Files`文件夹。

将在即将发布的服务版本中解决此问题。 一种解决方法，提供组， **SQLRUserGroup**，具有针对所有父文件夹的读取访问`ExternalLibraries`。

**RevoScaleR 版本旧和新版本之间的序列化错误**


如果你通过使用远程 SQL Server 实例的序列化的格式的模型，你可能会出现错误：

> *MemDecompress 中的错误 (数据、 类型 = 解压缩) memDecompress(2) 中的内部错误-3。*

如果保存模型时使用了新版本的序列化函数中，会出现此错误[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，但其中你进行反序列化模型的 SQL Server 实例已 RevoScaleR Api，请从 SQL 的旧版本Server 2017 CU2 或更早版本。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-converting-r-code-for-execution-in-databaserconverting-r-code-for-use-in-sql-servermd"></a>2.&nbsp; [转换执行数据库中的 R 代码](r/converting-r-code-for-use-in-sql-server.md)

*更新时间： 2018年-01-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 136.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a1d156fac1af5813ef75965071686b177e2aede7 fc8beff0aa0d7ea298e493b90984875e81e9143e  (PR=4493  ,  Filename=converting-r-code-for-use-in-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f486d12078a45c87b0fcf52270b904ca7b0c7fc8) -->



**包中的存储过程的 R 代码**

+ 如果代码是相对简单，你可以将其嵌入 T-SQL 的用户定义函数而不进行修改中,，这些示例中所述：

    + [创建在 rxExec 中运行的 R 函数](r/../tutorials/deepdive-create-a-simple-simulation.md)
    + [使用 T-SQL 和 R 的特征工程](r/../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 如果更复杂的代码，则使用 R 包**sqlrutils**要转换你的代码。 此包旨在帮助编写良好的存储的过程代码的有经验的 R 用户。

    第一步是重写 R 代码，作为单个函数具有明确定义的输入和输出。

    然后，使用**sqlrutils**包以正确的格式生成的输入和输出。 **Sqlrutils**包为你生成的完整存储的过程代码和还可以在数据库中注册该存储的过程。

    有关详细信息和示例，请参阅[SqlRUtils](r/../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。

**与其他工作流集成**

+ 利用 T-SQL 的工具和 ETL 过程。 执行特征工程、 功能提取和数据清理提前数据工作流的一部分。

    当你处理的专用的 R 开发环境，例如 R Tools for Visual Studio 或 RStudio 时, 可能到你的计算机中提取数据、 以迭代方式，分析数据，然后写出或显示的结果。

    但是，当独立 R 代码迁移到 SQL Server 中，此过程的大部分可简化或委派给其他 SQL Server 工具。

+ 使用安全、 异步可视化效果策略。

    SQL Server 的用户通常无法访问在服务器上，文件和 SQL 客户端工具通常不支持 R 图形设备。 如果你生成图形或其他图形作为解决方案的一部分，请考虑为二进制数据导出绘图和保存到表，或者通过编写。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3.&nbsp; [确定 SQL 服务器上安装哪些 R 包](r/determine-which-packages-are-installed-on-sql-server.md)

*更新时间： 2018年-01-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2))

<!-- Source markdown line 78.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9a065066398843a4bed318fa46d4982d712915a9 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f  (PR=4715  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=9e6a029456f4a8daddb396bc45d7874a43a47b45) -->




**获取库位置和版本**


下面的示例获取在本地计算上下文中，以及程序包版本 RevoScaleR 的库位置。

```
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

**确定 SQL Server 使用的库路径**


如果你已升级机器学习使用绑定的组件，可能会更改 R 库的路径。 在此情况下，R 工具的以前快捷方式可能引用的早期版本。 若要确保的 SQL Server 使用的路径和包版本，你可以运行如下命令：

```
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**结果**

```
STDOUT message(s) from external script:
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章


- [新文章和更新的文章 (1+3)：SQL&nbsp;高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章和更新的文章 (0+1)：SQL&nbsp;分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章和更新的文章 (0+1)：连接到&nbsp;SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (0+1)：SQL&nbsp;数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (12+1)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章&nbsp;(6+2)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (15+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章&nbsp;(2+9)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章&nbsp;(1+0)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章&nbsp;(1+1)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章和更新的文章&nbsp;(1+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新文章和更新的文章&nbsp;(0+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章&nbsp;(1+2)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章&nbsp;(0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章


- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX 数据对象 (ADO) sql**文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (0 + 0): **sql Data Quality Services**文档](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**数据挖掘扩展插件 (DMX) sql**文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多维表达式 (MDX) sql**文档](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **sql 的 ODBC （开放式数据库连接）**文档](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0): **SQL 的示例**文档](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **SQL 的 XQuery**文档](../xquery/new-updated-xquery.md)


