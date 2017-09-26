---
title: "已更新 - SQL Server 文档 | Microsoft Docs"
description: "显示 SQL Serverl 文档中最近更改的更新内容片段。"
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
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 7f1c64e11e1bec44a558cec10c3d1f90f4951dfd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>新文章和最近更新的文章：SQL Server 文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-07-18 到 2017-09-11
- 主题领域：&nbsp;**SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [SQL Server 2008 R2 SP2 Release Notes](sql-server-2008-r2-sp2-release-notes.md)
2. [SQL Server 2012 发行说明](sql-server-2012-release-notes.md)
3. [SQL Server 2012 SP1 Release Notes](sql-server-2012-sp1-release-notes.md)
4. [SQL Server 2012 SP2 Release Notes](sql-server-2012-sp2-release-notes.md)
5. [SQL Server 2012 SP3 发行说明](sql-server-2012-sp3-release-notes.md)
6. [SQL Server 2014 Release Notes](sql-server-2014-release-notes.md)
7. [SQL Server 的帮助查看器和脱机内容](sql-server-help-installation.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [SQL Server 2016 中的新增功能](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-whats-new-in-sql-server-2016what-s-new-in-sql-server-2016md"></a>1.&nbsp;[SQL Server 2016 中的新增功能](what-s-new-in-sql-server-2016.md)

更新日期：2017-09-08 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 34.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e5bc0c05f120289f09a535400a4d521e4113ae55 0607d0a9af1c9a8dd9d3d7b0606895ff23bbffdc  (PR=0  ,  Filename=what-s-new-in-sql-server-2016.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



- 下载免费的 [SQL Server 2016 开发者版！](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers)
- 下载最新版 [SQL Server Management Studio (SSMS)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms)。
- 是否拥有 Azure 帐户？ 加速[已安装有 SQL Server 2016 的虚拟机](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)。

**SQL Server 2016 数据库引擎**

- 现在可以在 SQL Server 安装和设置过程中配置多个 tempDB 数据库文件。
- 新的“查询存储”在数据库中存储查询文本、执行计划和性能指标，以便于监视和排查性能问题。 仪表板可显示耗时最长、占用内存或 CPU 资源最多的查询。
- 时态表是记录所有数据更改（包括更改日期和时间）的历史记录表。
- SQL Server 中新增了内置 JSON 支持，可以支持 JSON 导入、导出、分析和存储。
- 新的 PolyBase 查询引擎将 SQL Server 与 Hadoop 或 Azure Blob 存储中的外部数据相集成。 可以导入和导出数据，也可以执行查询。
- 借助新增的 Stretch Database 功能，可以将本地 SQL Server 数据库中的数据动态安全地存档到云中的 Azure SQL 数据库。 SQL Server 会自动查询本地数据和链接数据库中的远程数据。
- **内存中 OLTP：**
    - 现在支持 FOREIGN KEY、UNIQUE 和 CHECK 约束，以及本地编译存储过程 OR、NOT、SELECT DISTINCT、OUTER JOIN 和 SELECT 中的子查询。
    - 支持最大 2TB 的表（之前为最大 256GB）。
    - 为了实现排序和 AlwaysOn 可用性组支持，增强了列存储索引。
- 新增安全功能：
    - **Always Encrypted：**启用后，只有具有加密密钥的应用程序，才能访问 SQL Server 2016 数据库中的加密敏感数据。 密钥绝不会传递给 SQL Server。







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (3+12)：SQL 高级分析 文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章和更新的文章 (5+0)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (5+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (19+82)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (1+8)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (12+1)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (0+1)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (7+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新文章和更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章 (0+2)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (1+4)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (4+1)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)
- [新文章和更新的文章 (0+1)：Tools for SQL 文档](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



