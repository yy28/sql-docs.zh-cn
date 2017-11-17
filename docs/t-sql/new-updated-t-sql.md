---
title: "已更新-T-SQL 的文档 |Microsoft 文档"
description: "显示更新内容的最近更改中的文档，对于 TRANSACT-SQL 代码的段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: t-sql
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.author: genemi
ms.workload: t-sql
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 4d48c7df783ebe50f7b5d7fe3e72bef91559006e
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的和最近的更新： TRANSACT-SQL 的文档
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]


Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *日期范围的更新：* &nbsp; **自 2017 年 1-09-11** &nbsp;到&nbsp;**自 2017 年 1-09-27**
- *主题区域：* &nbsp; **T-SQL**。




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

1. [sql_variant (TRANSACT-SQL)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sqlvariant-transact-sqldata-typessql-variant-transact-sqlmd"></a>1. &nbsp; [sql_variant (TRANSACT-SQL)](data-types/sql-variant-transact-sql.md)

*更新时间： 2017年-09-13* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 111.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 659578de7de33d8672ceb9542093862107d13526 c80026de2b0deedab3722a874e9124c2cfefa049  (PR=0  ,  Filename=sql-variant-transact-sql.md  ,  Dirpath=docs\t-sql\data-types\  ,  MergeCommitSha40=5cd78481b3fac55ec34b59e7b1ad25e0e14d2a00) -->



**示例**


**A.表中使用 sql_variant**

 下面的示例中，创建了 sql_variant 数据类型的表。 然后该示例将检索`SQL_VARIANT_PROPERTY`有关的信息`colA`值`46279.1`其中`colB`  = `1689`，鉴于`tableA`具有`colA`类型`sql_variant`和`colB`.

```
CREATE   TABLE tableA(colA sql_variant, colB int)
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'
FROM      tableA
WHERE      colB = 1689
```

 ..!包括 NotShown-ssResult.../../includes/ssresult-md.md)] 请注意，其中每个三个值是**sql_variant**。

```
Base Type    Precision    Scale
---------    ---------    -----
decimal      8           2

(1 row(s) affected)
```

**B.使用 sql_variant 作为变量**

 以下示例中，创建使用 sql_variant 数据类型、 一个变量，然后检索`SQL_VARIANT_PROPERTY`有关名为变量的信息@v1。

```
DECLARE @v1 sql_variant;
SET @v1 = 'ABC';
SELECT @v1;
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');
```








## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (0 + 1): **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (0 + 1): **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (4 + 1): **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (17 + 0): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (3 + 0): **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (1 + 1): **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (2 + 0): **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 1): **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 1): **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+0)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (0 + 0): **SQL 的工具**文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



