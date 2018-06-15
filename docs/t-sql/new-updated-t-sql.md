---
title: 已更新 - T-SQL 文档 | Microsoft Docs
description: 显示 Transact-SQL 文档中最近更改的更新内容片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 04/28/2018
ms.openlocfilehash: b1bc891bf7edc4cd82c38c8d647c279828190298
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32725619"
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的和最近更新的文章：Transact-SQL 文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题区域：&nbsp; T-SQL。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


暂时无新文章列出。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](#TitleNum_1)
2. [RESTORE 语句 (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-alter-database-scoped-configuration-transact-sqlstatementsalter-database-scoped-configuration-transact-sqlmd"></a>1.&nbsp; [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](statements/alter-database-scoped-configuration-transact-sql.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

<!-- Source markdown line 150.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f6833910b664d0059a9073589807b195052325b3 bf969f123b22e6ebc650380a6905156f26ed6ca6  (PR=0  ,  Filename=alter-database-scoped-configuration-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



XTP_PROCEDURE_EXECUTION_STATISTICS  = { ON | OFF }

适用于：{Included-Content-Goes-Here}

启用或禁用对当前数据库的本机编译的 T-SQL 模块在模块级别的执行统计信息收集。 默认为 OFF。 执行统计信息反映在 [sys.dm_exec_procedure_stats] 中。

如果该选项为“开”，或通过 [sp_xtp_control_proc_exec_stats] 启用了统计信息收集，则收集对本机编译的 T-SQL 模块的模块级别执行统计信息。

XTP_QUERY_EXECUTION_STATISTICS  = { ON | OFF }

适用于：{Included-Content-Goes-Here}

启用或禁用对当前数据库的本机编译的 T-SQL 模块语句级别的执行统计信息收集。 默认为 OFF。 执行统计信息反映在 [sys.dm_exec_query_stats] 和[查询存储]中。

如果该选项为“开”，或通过 [sp_xtp_control_query_exec_stats] 启用了统计信息收集，则收集对本机编译的 T-SQL 模块的语句级别执行统计信息。

有关本机编译的 T-SQL 模块的性能监视的详细信息，请参阅[监视本机编译的存储过程的执行]。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-restore-statements-transact-sqlstatementsrestore-statements-transact-sqlmd"></a>2.&nbsp; [RESTORE 语句 (Transact-SQL)](statements/restore-statements-transact-sql.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_1))

<!-- Source markdown line 339.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2902efb58bb964d3e9a0660956690d37f0397c00 36186a7cffd26ffa54a83e383ffd752dbc568a4d  (PR=0  ,  Filename=restore-statements-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**一般注释 - SQL 数据库托管实例**


对于异步还原，即使客户端连接中断，还原操作也会继续运行。 如果连接断开，可检查 [sys.dm_operation_status] 视图，查看还原操作的状态（以及查看 CREATE 和 DROP 数据库）。

已设置/覆盖以下数据库选项，这些选项稍后无法进行更改：

- NEW_BROKER（如果 .bak 文件中未启用中转站）
- ENABLE_BROKER（如果 .bak 文件中未启用中转站）
- AUTO_CLOSE=OFF（如果 .bak 文件中的数据库具有 AUTO_CLOSE=ON）
- RECOVERY FULL（如果 .bak 文件中的数据库具有 SIMPLE 或 BULK_LOGGED 恢复模式）
- 如果源 .bak 文件中不存在内存优化文件组，则会添加一个，并将其命名为 XTP。 任何现有内存优化文件组都会重命名为 XTP
- SINGLE_USER 和 RESTRICTED_USER 选项会转换为 MULTI_USER

**限制 - SQL 数据库托管实例**

这些限制包括：

- 无法还原包含多个备份集的 .BAK 文件。
- 无法还原包含多个日志文件的 .BAK 文件。
- 如果 .bak 中包含 FILESTREAM 数据，则还原将失败。
- 如果备份中包含的数据库具有活动的内存中对象，则该备份当前无法还原。
- 如果备份中包含的数据库中某些时候存在内存中对象，则该备份当前无法还原。
- 如果备份包含处于只读模式的数据库，则该备份当前无法还原。 此限制很快就会取消。

有关详细信息，请参阅[托管实例]







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

