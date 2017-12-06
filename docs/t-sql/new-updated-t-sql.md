---
title: "已更新-T-SQL 的文档 |Microsoft 文档"
description: "显示更新内容的最近更改中的文档，对于 TRANSACT-SQL 代码的段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: t-sql
ms.openlocfilehash: 33c50454f34c1902ea7f7dedc9ecb0a54f99ce24
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的和最近的更新： TRANSACT-SQL 的文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *日期范围的更新：* &nbsp; **自 2017 年 1-09-28** &nbsp;到&nbsp;**自 2017 年 1-12-02**
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

1. [反斜杠 （续行符） (Transact SQL)](#TitleNum_1)
2. [SELECT-ORDER BY 子句 (TRANSACT-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-backslash-line-continuation-transact-sqllanguage-elementssql-server-utilities-statements-backslashmd"></a>1.&nbsp;[反斜杠 （续行符） (Transact SQL)](language-elements/sql-server-utilities-statements-backslash.md)

*更新时间： 自 2017 年 1-11-15* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 83.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9484441710ac9a083a554ffadb59a3b7e92484b3 19b9c37c65ba462a32067c80e81a920eeb339851  (PR=3966  ,  Filename=sql-server-utilities-statements-backslash.md  ,  Dirpath=docs\t-sql\language-elements\  ,  MergeCommitSha40=b0c223ba0f78af5eb76948e68e2d1aab2e7b80c1) -->



**B.将二进制字符串拆分**


下面的示例使用一个反斜杠和回车二进制字符串拆分为两行。

```
SELECT 0xabc\
def AS [ColumnResult];

```

 ..!包括 NotShown-ssResult.../../includes/ssresult-md.md)]

```
 ColumnResult
 ------------
 0xABCDEF
```




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-select---order-by-clause-transact-sqlqueriesselect-order-by-clause-transact-sqlmd"></a>2.&nbsp;[选择-ORDER BY 子句 (TRANSACT-SQL)](queries/select-order-by-clause-transact-sql.md)

*更新时间： 自 2017 年 1-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1))

<!-- Source markdown line 481.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b8d7bc7bab46e914eb2facf6c654a5944383077e de7e4f3f7826011e273120a2b6b08af4d263a510  (PR=3663  ,  Filename=select-order-by-clause-transact-sql.md  ,  Dirpath=docs\t-sql\queries\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



**<a name="Union"></a>使用联合的 ORDER BY，除非和 INTERSECT**

 当查询使用 UNION、EXCEPT 或 INTERSECT 运算符时，必须在语句末尾指定 ORDER BY 子句，并对合并的查询结果进行排序。 以下示例返回所有红色或黄色的产品，并按 `ListPrice` 列对合并的列表进行排序。

```sql
USE AdventureWorks2012;
GO
SELECT Name, Color, ListPrice
FROM Production.Product
WHERE Color = 'Red'
-- ORDER BY cannot be specified here.
UNION ALL
SELECT Name, Color, ListPrice
FROM Production.Product
WHERE Color = 'Yellow'
ORDER BY ListPrice ASC;

```

**示例:..！包括 NotShown-ssSDWfull.../../includes/sssdwfull-md.md)] 和..！包括 NotShown-ssPDW.../../includes/sspdw-md.md)]**








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


