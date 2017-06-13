---
title: "已更新-SQL Server 文档 |Microsoft 文档"
description: "显示更新内容的 SQL Server 的最近更改中文档的代码的段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 7fba3b05943b93c0a2c0e76c2d0d5f2696a48d1c
ms.contentlocale: zh-cn
ms.lasthandoff: 05/25/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>新的和最近的更新： SQL Server 文档



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- *日期范围的更新：* &nbsp; **自 2017 年 1-05-01** &nbsp;到&nbsp;**自 2017 年 1-05-23**
- *主题区域：* &nbsp; **SQL Server**。




&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1.&nbsp;[SQL Server 自 2017 年 1 发行说明](sql-server-2017-release-notes.md)

*Updated: 2017-05-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 84e7a2a49f2893d49380db1ad75695d9a4fd59b2 27a145ad30c10fd667f926d2e092b88c0ba586c5 -->



**SQL Server 自 2017 年 1 CTP 2.1 (2017 年 5 月)**

**文档 (CTP 2.1)**

- **问题及其对客户的影响：**文档 [！包括 [ssSQLv14_md.../includes/sssqlv14-md.md)] 是有限，包含与内容 [！包括 [ssSQL15_md.../includes/sssql15-md.md)] 文档集。  内容的项目中的特定于 [！包括 [ssSQLv14_md...将与记录 /includes/sssqlv14-md.md)]**适用于**。 
- **问题及其对客户的影响：**没有脱机内容是可用于 [！包括 [ssSQLv14_md.../includes/sssqlv14-md.md)]。

**SQL Server Reporting Services (CTP 2.1)**


- **问题及其对客户的影响：**如果你有 SQL Server Reporting Services 和 Power BI 报表服务器在同一计算机，并且卸载其中之一，你将不再能够连接到剩余的报表服务器与报表服务器配置管理器中。
- **解决方法**若要解决此问题，你必须卸载服务器之一后执行以下操作。

    1. 在管理员模式下启动命令提示符。
    2. 转到安装其余报表服务器的目录。

        *Power BI 报表服务器的默认位置： C:\Program Files\Microsoft Power BI 报表服务器*

        *SQL Server Reporting Services 的默认位置： C:\Program Files\Microsoft SQL Server Reporting Services*

    3. 然后转到下一个文件夹。 该地址可以是*SSRS*或*PBIRS*具体取决于什么剩余。
    4. 转到 WMI 文件夹。
    5. 运行以下命令：

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        如果看到它，可忽略以下错误。

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

**TSqlLanguageService.msi (CTP 2.1)**


- **问题及其对客户的影响：**后具有 2016年版本的计算机上安装*TSqlLanguageService.msi* v13.* (SQL 2016) 版本的安装 （通过 SQL 安装程序或作为独立的可再发行组件） *Microsoft.SqlServer.Management.SqlParser.dll*和*Microsoft.SqlServer.Management.SystemMetadataProvider.dll*会删除。 任何应用程序依赖于这些程序集的 2016年版本将然后停止正常运行，提供如下错误：*错误： 无法加载文件或程序集 Microsoft.SqlServer.Management.SqlParser，Version = 13.0.0.0，区域性 = neutral，PublicKeyToken = 89845dcd8080cc91 或其依赖项之一。系统找不到指定的文件。*




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-what39s-new-in-sql-server-2017what-s-new-in-sql-server-2017md"></a>2.&nbsp;[什么 &#39; s SQL Server 自 2017 年中的新增功能](what-s-new-in-sql-server-2017.md)

*Updated: 2017-05-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 31.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b3e965f62414af06d42f88497958a4bca67befce 82ad09ae9a917f26db3e2210b5cf89585e0e4c4e -->



**什么是 SQL Server 自 2017 年 1 CTP 2.1 (5 月 2017) 中的新增功能**

* * SQL Server 数据库引擎 * *

- 新的 DMF，[sys.dm_db_log_stats.../ relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md），引入公开摘要级别的特性和事务日志文件; 上的信息用于监视事务日志的运行状况。  
- 此 CTP 包含对数据库引擎的 bug 修复和性能改进。
- 有关自 2017 年 1 的详细列表 CTP 增强功能在以前的 CTP 版本，请参阅 [What's New in SQL Server 2017 （数据库引擎）.../ database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md）。

**SQL Server Reporting Services (SSRS)**

- SQL Server Reporting Services 不再可用于通过截至 CTP 2.1 的 SQL Server 安装程序安装。
- 批注现可用于报表。 通过批注，可向报表中的内容添加透视图并与组织中的其他人进行协作。 还可在批注中包含附件。
- 对于更详细的 SSRS 是什么新信息，包括从以前版本的详细信息，请参阅 [什么是新在 Reporting Services.../ reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md）。 
- 有关 Power BI 报表服务器的信息，请参阅[开始使用 Power BI 报表服务器](https://powerbi.microsoft.com/documentation/reportserver-get-started/)。

**SQL Server 机器学习服务**

- 在此 CTP 中没有新机器学习服务功能。
- 对于更详细的机器学习服务是什么新信息，包括从以前的 Ctp 详细信息，请参阅 [什么是新建中 SQL Server 机器学习服务.../ advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md）。  

**SQL Server Analysis Services (SSAS)**

- 此 CTP 中没有新的 SSAS 功能。  
- 有关改进和 bug 修复，在此版本的详细信息，请参阅 [新增功能在 SQL Server 自 2017 年 Analysis Services.../ analysis-services/what-s-new-in-sql-server-analysis-services-2017.md）。  





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此 compact 列表提供了在上一节中列出的所有更新文章的链接。

1. [SQL Server 自 2017 年 1 发行说明](#TitleNum_1)
2. [什么 &#39; s SQL Server 自 2017 年中的新增功能](#TitleNum_2)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>相关文章

本部分列出了一些相同的 GitHub 存储库中的其他使用者区域中的最近更新项目非常相似文章。


&nbsp;

[Microsoft /**sql 文档 pr** ](https://github.com/microsoftdocs/sql-docs-pr/) GitHub.com 上的存储库：

- [最近更新：**关系数据库和 Microsoft SQL Server**文档](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [最近更新： **Microsoft SQL Server**文档](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [最近更新： **TRANSACT-SQL 在 SQL Server 中**文档](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



