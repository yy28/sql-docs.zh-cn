---
title: 计算列上的索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ffa842513c5cd185c7760bc737aeb64a4c33742e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279113"
---
# <a name="indexes-on-computed-columns"></a>计算列上的索引
  只要满足下列要求就可以为计算列定义索引：  
  
-   所有权要求  
  
-   确定性要求  
  
-   精度要求  
  
-   数据类型要求  
  
-   SET 选项要求  
  
 **Ownership Requirements**  
  
 计算列中的所有函数引用必须与表具有相同的所有者。  
  
 **Determinism Requirements**  
  
> [!IMPORTANT]  
>  如果对于一组指定的输入表达式始终返回相同的结果，则说明表达式具有确定性。 **COLUMNPROPERTY** 函数的 [IsDeterministic](/sql/t-sql/functions/columnproperty-transact-sql) 属性报告 *computed_column_expression* 是否具有确定性。  
  
 *Computed_column_expression* 必须具有确定性。 如果下列一项或多项为真，则 *computed_column_expression* 具有确定性：  
  
-   表达式引用的所有函数都具有确定性，并且是精确的。 这些函数包括用户定义函数和内置函数。 有关详细信息，请参阅 [Deterministic and Nondeterministic Functions](../user-defined-functions/deterministic-and-nondeterministic-functions.md)。 如果计算列是 PERSISTED，则函数可能不精确。 有关详细信息，请参阅本主题后面的 [对持久化计算列创建索引](#BKMK_persisted) 。  
  
-   表达式引用的所有列都来自包含计算列的表。  
  
-   没有列引用从多行中请求数据。 例如，聚合函数（如 SUM 或 AVG）依靠来自多行的数据，这使 *computed_column_expression* 具有不确定性。  
  
-   *computed_column_expression* 没有系统数据访问或用户数据访问。  
  
 任何包含公共语言运行时 (CLR) 表达式的计算列都必须具有确定性并标记为 PERSISTED，这样才能为该列创建索引。 允许在计算列定义中使用 CLR 用户定义类型的表达式。 类型为 CLR 用户定义类型的计算列只要其类型是可比较的，就可以在该列上创建索引。 有关详细信息，请参阅 [CLR 用户定义类型](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
> [!NOTE]  
>  如果您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内的索引计算列中引用 date 数据类型的字符串文字，则建议使用确定性日期格式样式将该文字显式转换为所需的日期类型。 有关确定性日期格式样式的列表，请参阅 [CAST and CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql)。 除非数据库兼容级别设置为 80 或更低，否则涉及字符串到 date 数据类型的隐式转换的表达式将被视为具有不确定性。 这是因为结果取决于服务器会话的 [LANGUAGE](/sql/t-sql/statements/set-language-transact-sql) 和 [DATEFORMAT](/sql/t-sql/statements/set-dateformat-transact-sql) 设置。 例如，表达式 `CONVERT (datetime, '30 listopad 1996', 113)` 的结果取决于 LANGUAGE 设置，因为字符串`30 listopad 1996`在不同语言中表示不同的月份。 同样，在表达式 `DATEADD(mm,3,'2000-12-01')`中， [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 基于 DATEFORMAT 设置解释字符串 `'2000-12-01'` 。  
>   
>  非 Unicode 字符数据在排序规则间的隐式转换也被视为具有不确定性，除非兼容级别设置为 80 或更低。  
>   
>  当数据库兼容级别设置为 90 时，不能对包含这些表达式的计算列创建索引。 但在已升级的数据库中，包含这些表达式的现有计算列是可以维护的。 如果使用包含字符串到日期的隐式转换的索引计算列，则为了避免损坏索引，请确保数据库和应用程序中的 LANGUAGE 和 DATEFORMAT 设置一致。  
  
 **Precision Requirements**  
  
 *computed_column_expression* 必须精确。 如果下列一项或多项为真，则 *computed_column_expression* 是精确的：  
  
-   表达式的数据类型不是 `float` 或 `real`。  
  
-   它不使用`float`或`real`在其定义中的数据类型。 例如，在下面的语句中，列`y`是`int`和具有确定性，但不是精确。  
  
    ```  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
>  任何`float`或`real`表达式被视为不精确，不能为索引键;`float`或`real`索引视图中，但不是作为键，可以使用表达式。 对于计算列同样如此。 任何函数、 表达式或用户定义函数被视为不精确，如果它包含任何`float`或`real`表达式。 这也包括逻辑表达式（比较）。  
  
 COLUMNPROPERTY 函数的 **IsPrecise** 属性报告 *computed_column_expression* 是否精确。  
  
 **Data Type Requirements**  
  
-   *Computed_column_expression*为计算的列的值不能为定义`text`， `ntext`，或`image`数据类型。  
  
-   从派生的计算列`image`， `ntext`， `text`， `varchar(max)`， `nvarchar(max)`， `varbinary(max)`，和`xml`可索引数据类型，只要计算的列数据类型作为索引键列。  
  
-   从派生的计算列`image`， `ntext`，和`text`数据类型可以是在非聚集索引的键 （包含） 列，只要计算的列数据类型作为非键索引列。  
  
 **SET Option Requirements**  
  
-   执行定义计算列的 CREATE TABLE 或 ALTER TABLE 语句时，必须将 ANSI_NULLS 连接级选项设置为 ON。 [OBJECTPROPERTY](/sql/t-sql/functions/objectpropertyex-transact-sql) 函数通过 **IsAnsiNullsOn** 属性报告此选项是否设置为 ON。  
  
-   对于在其中创建索引的连接和所有尝试执行 INSERT、UPDATE 或 DELETE 语句（将更改索引中的值）的连接，必须将六个 SET 选项设置为 ON，将一个选项设置为 OFF。 如果不具有上述选项设置的连接执行了任何 SELECT 语句，优化器将忽略计算列的索引。  
  
    -   NUMERIC_ROUNDABORT 选项必须设置为 OFF，且下列选项必须设置为 ON：  
  
    -   ANSI_NULLS  
  
    -   ANSI_PADDING  
  
    -   ANSI_WARNINGS  
  
    -   ARITHABORT  
  
    -   CONCAT_NULL_YIELDS_NULL  
  
    -   QUOTED_IDENTIFIER  
  
     当数据库兼容级别设置为 90 或更高时，如果将 ANSI_WARNINGS 设置为 ON，则将使 ARITHABORT 隐式设置为 ON。  
  
##  <a name="BKMK_persisted"></a> 对持久化计算列创建索引  
 如果计算列使用确定性但不精确的表达式定义，但在 CREATE TABLE 或 ALTER TABLE 语句中标记为 PERSISTED，则可以在该列上创建索引。 这意味着，[!INCLUDE[ssDE](../../../includes/ssde-md.md)]对列创建索引时和在查询中引用的索引时使用这些持久的值。 此选项可以对计算列创建索引时[!INCLUDE[ssDE](../../../includes/dnprdnshort-md.md)]，是具有确定性并精确。  
  
## <a name="related-content"></a>相关内容  
 [COLUMNPROPERTY (Transact-SQL)](/sql/t-sql/functions/columnproperty-transact-sql)  
  
  
