---
title: "更新的示例性 SQL Server 文档 |Microsoft 文档"
description: "显示更新内容的最近更改中的文档，Microsoft SQL server 示例的代码的段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: samples
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: sample
ms.openlocfilehash: 363cb5dde93c628317a977082fe8697af890d51c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sample-for-sql-server"></a>新的和最近的更新： SQL Server 的示例



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *日期范围的更新：* &nbsp; **自 2017 年 1-09-28** &nbsp;到&nbsp;**自 2017 年 1-12-02**
- *主题区域：* &nbsp; **用于 SQL Server 示例**。




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

1. [WideWorldImporters 数据库目录](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-wideworldimporters-database-catalogworld-wide-importersdatabase-catalog-oltpmd"></a>1.&nbsp;[WideWorldImporters 数据库目录](world-wide-importers/database-catalog-oltp.md)

*更新时间： 自 2017 年 1-11-20* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 136.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c055d0483699f06b8766ac2c999101934c14c55c 6975d5a3d1ade7b0ce34bd165bc0e9ef49299ba2  (PR=4032  ,  Filename=database-catalog-oltp.md  ,  Dirpath=docs\sample\world-wide-importers\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



只要有可能，数据库将配置到相同的架构，以最小化联接复杂性常用查询的表。

数据库架构已生成的代码基于一系列的另一个数据库 WWI_Preparation 中的元数据表。 这样，WideWorldImporters 非常高的设计的一致性，命名一致性和完整性。 有关如何生成架构的详细信息，请参阅源代码：[范围的实际-导入程序/wwi-数据库的脚本](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

**表设计**


- 所有表都具有单个列主键联接为了简单起见。
- 所有架构、 表、 列、 索引和检查约束都具有扩展属性，可以用于标识对象或列的用途的说明。 内存优化表是一种例外，因为它们当前不支持扩展的属性。
- 如果没有具有相同的左侧组件的另一个非聚集索引，所有外键会自动编制索引。
- 表中自动编号取决于序列。 更轻松地使用跨链接的服务器和与标识列的类似环境中这些序列。 内存优化表使用标识列，因为它们不支持在 SQL Server 2016 中。
- 一个序列 (TransactionID) 用于这些表： CustomerTransactions、 SupplierTransactions 和 StockItemTransactions。 此示例演示如何一组表可以有一个序列。
- 某些列具有适当的默认值。

**安全架构**


为安全起见，WideWorldImporters 不允许外部应用程序直接访问数据架构。 若要隔离访问，WideWorldImporters，请使用安全访问架构不具有相关数据，但包含视图和存储的过程。 外部应用程序使用的安全架构检索允许他们查看的数据。  这样一来，用户只能运行的视图和存储的过程中的安全访问架构







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (3 + 14): **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新的和更新的文章 (1+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (87 + 0): **SQL 的分析平台系统**文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (5 + 4):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1): **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (2 + 2): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (10 + 9): **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (2 + 4): **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (4 + 2): **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 1): **SQL 的示例**文档](../sample/new-updated-sample.md)
- [新 + 更新 (21 + 0): **SQL 操作 Studio**文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (5 + 1): **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+1)：SQL Server Data Tool (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 0): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新 + 更新 (0 + 0):**数据迁移助手 (DMA) sql**文档](../dma/new-updated-dma.md)
- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


