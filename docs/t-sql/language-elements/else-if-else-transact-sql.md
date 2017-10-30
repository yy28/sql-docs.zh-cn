---
title: "其他 (IF...其他） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18adc4f441fddecdb3cd96c2a253268a16daea46
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="else-ifelse-transact-sql"></a>ELSE (IF...ELSE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的执行条件。 [!INCLUDE[tsql](../../includes/tsql-md.md)]语句 (*sql_statement*) 以下*Boolean_expression*如果执行*Boolean_expression*计算结果为 TRUE。 可选的 ELSE 关键字是一个备选[!INCLUDE[tsql](../../includes/tsql-md.md)]语句时执行*Boolean_expression*计算结果为 FALSE 或 NULL。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>参数  
 *Boolean_expression*  
 返回 TRUE 或 FALSE 的表达式。 如果*Boolean_expression*包含 SELECT 语句，SELECT 语句必须括在括号中。  
  
 { *sql_statement* | *statement_block* }  
 任何有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或用语句块定义的语句分组。 若要定义语句块（批处理），请使用控制流语言关键字 BEGIN 和 END。 虽然所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在 BEGIN...END 块内都有效，但有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句不能组合到同一个批（语句块）中。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. 使用简单的布尔表达式  
 下面的示例具有一个为 True 的简单布尔表达式 (`1=1`)，因此打印第一条语句。  
  
```  
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 下面的示例具有为 False 的简单布尔表达式 (`1=2`)，因此打印第二条语句。  
  
```  
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>B. 将查询用作布尔表达式的一部分  
 下面的示例执行属于布尔表达式一部分的查询。 由于 `Product` 表中有 10 辆符合 `WHERE` 子句条件的自行车，因此将执行第一条打印语句。 将 `> 5` 更改为 `> 15` 查看如何执行第二部分语句。  
  
```  
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. 使用语句块  
 下面的示例执行属于布尔表达式一部分的查询，然后再根据布尔表达式的结果执行稍有不同的语句块。 每个语句块以 `BEGIN` 开头，并以 `END` 结束。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight decimal(8,2), @BikeCount int  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS varchar(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. 使用嵌套的 IF...ELSE 语句  
 下面的示例显示如何 IF... ELSE 语句可以嵌套在另一个。 将 `@Number` 变量设置为 `5`、`50` 和 `500` 以测试每个语句。  
  
```  
DECLARE @Number int;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E： 作为布尔表达式的一部分使用查询  
 下面的示例使用`IF…ELSE`根据中的项的权重来确定这两个响应以向用户，`DimProduct`表。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE (Transact-SQL)](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  



