---
title: 已更新 - 适用于 SQL Server 的 SSMS 文档 | Microsoft Docs
description: 显示 SQL Server 的 SQL Server Management Studio (SSMS) 文档中最近更改的更新内容片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 04/28/2018
ms.openlocfilehash: 1ce446219f71baca0f4cdedc835fca929b572a0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>新的和最近更新的文章：适用于 SQL Server 的 SQL Server Management Studio (SSMS)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题区域： &nbsp; **SQL Server Management Studio (SSMS)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [教程：使用 SQL Server Management Studio 连接和查询 SQL Server 实例](tutorials/connect-query-sql-server.md)
2. [教程：在 SQL Server Management Studio 中编写对象脚本](tutorials/scripting-ssms.md)
3. [教程：SQL Server Management Studio 组件和配置](tutorials/ssms-configuration.md)
4. [教程：使用 SSMS 的其他提示和技巧](tutorials/ssms-tricks.md)
5. [教程：在 SQL Server Management Studio 中使用模板](tutorials/templates-ssms.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [SQL Server Management Studio (SSMS) - 更改日志](#TitleNum_1)
2. [SQL Server Management Studio (SSMS) 教程](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>1.&nbsp; [SQL Server Management Studio - 更改日志 (SSMS)](sql-server-management-studio-changelog-ssms.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 eb641ac39386a26a76dc303f5bd55eb3f9f4c78d f560f09b51ea30b255c10f7eb86857c3090881d9  (PR=5676  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[SSMS 17.6]**


版本号：17.6<br>
生成号：14.0.17230.0<br>
发布日期：2018 年 3 月 20 日

**新增功能**


**常规 SSMS**

SQL 数据库托管实例：

- 添加了对 [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)的支持。 Azure SQL 数据库托管实例（预览版）是 Azure SQL 数据库的一种新风格，提供与本地 SQL Server 的接近 100% 的兼容性，是一个解决常见安全问题的本机[虚拟网络 (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 实现和一个有利于本地 SQL Server 客户的[业务模型](https://azure.microsoft.com/pricing/details/sql-database/)。
- 支持常见管理方案，例如：
   - 创建和更改数据库。
   - 备份和还原数据库。
   - 导入、导出、提取和发布数据层应用程序。
   - 查看和更改服务器属性。
   - 完全支持对象资源管理器。
   - 编写数据库对象的脚本。
   - 支持 SQL 代理作业。
   - 支持链接服务器。
- 在[此处](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/)了解有关托管实例的更多信息。

对象资源管理器：
- 添加了设置，以便在从对象资源管理器拖放至查询窗口时，不强制使用括号括住名称。 （用户建议 [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) 和 [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051)。）

数据分类：
- 一般改进和 bug 修复。

**Integration Services (IS)**

- 添加了支持，便于将包部署到 [SQL 数据库托管实例](docs/ssms/https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tutorials-for-sql-server-management-studio-ssmstutorialstutorial-sql-server-management-studiomd"></a>2.&nbsp; [SQL Server Management Studio (SSMS) 教程](tutorials/tutorial-sql-server-management-studio.md)

更新日期：2018-04-25 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_1))

<!-- Source markdown line 49.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b272c75bab04912ebb706098cf6b6a6c80d9e2b8 d453ebc8251fb83ffcb1af58c9a08bb65b3e9fa2  (PR=5676  ,  Filename=tutorial-sql-server-management-studio.md  ,  Dirpath=docs\ssms\tutorials\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- 教程：使用 SSMS 连接并查询 SQL Server

    在本教程中，你将了解如何连接到 SQL Server 实例。 此外，你还将了解用于创建并查询新数据库的一些基本 Transact-SQL (T-SQL) 命令。

- 教程：在 SSMS 中编写对象脚本

    在本教程中，你将了解如何在 SSMS 中编写各种对象（包括数据库和查询）的脚本。

- 教程：在 SSMS 中使用模板

    在本教程中，你将了解如何使用 SSMS 中的预建模板。 模板是一项少有人知的功能，可针对各种数据库管理任务存储大量 Transact-SQL 代码片段。

- 教程：SSMS 配置

    本教程介绍有关如何配置 SSMS 环境（例如更改环境布局）的基础知识。 本教程还介绍各种不同的 SSMS 组件。


- 教程：使用 SSMS 的其他提示和技巧

    在本教程中，你将了解使用 SSMS 的其他提示和技巧。 本教程包括以下内容：
    - 注释和取消注释文本
    - 缩进文本
    - 在对象资源管理器中筛选对象
    - 访问 SQL Server 错误日志
    - 查找实例名称








## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (11+6)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)&nbsp; &nbsp;
- [新文章和更新的文章 (18+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (218+14)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (14+0)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+2)： SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+3)： Linux for SQL 文档](../linux/new-updated-linux.md)&nbsp; &nbsp;
- [新文章和更新的文章 (7+10)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Reporting Services for SQL 文档](../reporting-services/new-updated-reporting-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+3)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)&nbsp; &nbsp;
- [新文章和更新的文章 (2+3)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)&nbsp; &nbsp;
- [新文章和更新的文章 (5+2)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL 工具文档](../tools/new-updated-tools.md)&nbsp; &nbsp;



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章

- [新文章和更新的文章 (0+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../samples/new-updated-samples.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)

