---
title: 已更新 - 适用于 SQL Server 的 SSMS 文档 | Microsoft Docs
description: 显示 SQL Server 的 SQL Server Management Studio (SSMS) 文档中最近更改的更新内容片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: ssms
ms.date: 02/03/2018
ms.openlocfilehash: 8f2ad52b9741a3220a8c5db0a60924a41cc62d27
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>新的和最近更新的文章：适用于 SQL Server 的 SQL Server Management Studio (SSMS)



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：&nbsp;从 2017-12-03&nbsp; 到 2018-02-03&nbsp;
- 主题区域： &nbsp; **SQL Server Management Studio (SSMS)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [安装非英语语言版本的 SQL Server Management Studio (SSMS)](install-other-languages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [下载 SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [SQL Server Management Studio (SSMS) - 更改日志](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1.&nbsp;[下载 SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

更新日期：2018-01-18 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  （[下一篇](#TitleNum_2)）

<!-- Source markdown line 83.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0e123e7bdf04f02fcd26ac31fa30ed5f31b19c7d 924246b55d3cad6a5d068da8a41f4be23dcfeb2b  (PR=4652  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



SSMS 17.4 是 SQL Server Management Studio 的最新版本。 SSMS 的 17.x 一代提供对 SQL Server 2008 到 SQL Server 2017 几乎所有功能领域的支持。 版本 17.x 也支持 SQL Analysis Service PaaS。

版本 17.4 包括：

漏洞评估：
- 添加了一个新的 SQL 漏洞评估服务，以扫描数据库的潜在漏洞和最佳方案偏差，如配置错误、权限过多和敏感数据公开。
- 评估结果包括旨在解决每个问题的可操作步骤，并提供自定义修正脚本（若适用）。 可以为每个环境自定义评估报表并进行调整以满足特定需求。 访问 [SQL 漏洞评估](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)了解详细信息。

SMO：
- 修复了 HasMemoryOptimizedObjects 在 Azure 上引发异常的问题。
- 添加了对新 CATALOG_COLLATION 功能的支持。

AlwaysOn 仪表板：
- 可用性组中的延迟分析有所改进。
- 添加了两个新报表：AlwaysOn\_Latency\_Primary 和 AlwaysOn\_Latency\_Secondary。

Showplan：
- 已更新指向正确文档的链接。
- 允许直接从生成的实际计划进行单个计划分析。
- 新图标集。
- 添加了对识别 GbApply、InnerApply 等“应用逻辑运算符”的支持。

XE 探查器：
- 更名为 XEvent 探查器。
- 默认情况下，停止/启动菜单命令会立即停止/启动会话。
- 已启用键盘快捷方式（例如，用于搜索的 CTRL-F）。
- 向 XEvent 探查器会话中的相应事件添加了 database\_name 和 client\_hostname 操作。 为了使更改生效，你可能需要删除服务器上现有 QuickSessionStandard 或 QuickSessionTSQL 会话实例 - [连接 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>2.&nbsp; [SQL Server Management Studio - 更改日志 (SSMS)](sql-server-management-studio-changelog-ssms.md)

更新日期：2018-01-29 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  （[上一篇](#TitleNum_1)）

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5096fa8f1ae3f2e4bc040f43cb8810d96f2c69c eb641ac39386a26a76dc303f5bd55eb3f9f4c78d  (PR=0  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ba4b1c2e5200f2f78786b710da18fd38fedde6c9) -->



**[SSMS 17.4](download-sql-server-management-studio-ssms.md)**

正式发布版 | 内部版本号：14.0.17213.0

**新增功能**


**常规 SSMS**

漏洞评估：
- 添加了一个新的 SQL 漏洞评估服务，以扫描数据库的潜在漏洞和最佳方案偏差，如配置错误、权限过多和敏感数据公开。
- 评估结果包括旨在解决每个问题的可操作步骤，并提供自定义修正脚本（若适用）。 可以为每个环境自定义评估报表并进行调整以满足特定需求。 访问 [SQL 漏洞评估](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)了解详细信息。

SMO：
- 修复了 HasMemoryOptimizedObjects 在 Azure 上引发异常的问题。
- 添加了对新 CATALOG_COLLATION 功能的支持。

AlwaysOn 仪表板：
- 可用性组中的延迟分析有所改进。
- 添加了两个新报表：AlwaysOn\_Latency\_Primary 和 AlwaysOn\_Latency\_Secondary。

Showplan：
- 已更新指向正确文档的链接。
- 允许直接从生成的实际计划进行单个计划分析。
- 新图标集。
- 添加了对识别 GbApply、InnerApply 等“应用逻辑运算符”的支持。

XE 探查器：
- 更名为 XEvent 探查器。
- 默认情况下，停止/启动菜单命令会立即停止/启动会话。
- 已启用键盘快捷方式（例如，用于搜索的 CTRL-F）。
- 向 XEvent 探查器会话中的相应事件添加了 database\_name 和 client\_hostname 操作。 为了使更改生效，你可能需要删除服务器上现有 QuickSessionStandard 或 QuickSessionTSQL 会话实例 - [连接 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

命令行：
- 添加了新的命令行选项 (“-G”)，可以用于自动将 SSMS 连接到使用 Active Directory 身份验证（“集成”或“密码”）的服务器/数据库。 有关详细信息，请参阅 [Ssms 实用工具](ssms-utility.md)。







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
- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新文章和更新的文章 (0+0)：SQL Analysis Services 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../samples/new-updated-samples.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


