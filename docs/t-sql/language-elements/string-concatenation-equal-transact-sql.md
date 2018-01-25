---
title: "+ = （字符串串联和分配） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a1e42125e49b0191b4ccdcc3628b75d025cccb6a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+ = （字符串串联赋值） (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将两个字符串串联起来并将一个字符串设置为运算结果。 例如，如果变量@x等于 Adventure，然后@x+ = Works 采用的原始值@x，将工作原理添加到字符串，并设置@x为该新值 'AdventureWorks'。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任意字符数据类型。  
  
## <a name="result-types"></a>结果类型  
 返回为变量定义的数据类型。  
  
## <a name="remarks"></a>注释  
 设置@v1+ = expression 等效于组@v1= @v1 + （表达式）。 此外，还要设置@v1= @v2 + @v3 +@v4等效于集@v1= (@v2 + @v3) + @v4。  
  
 如果没有变量，则不能使用 += 运算符。 例如，下面的代码将导致错误：  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>示例  
### <a name="a-concatenation-using--operator"></a>A. 串联使用 + = 运算符
 下面的示例使用 `+=` 运算符进行串联。  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. 时串联使用 + = 运算符的计算顺序
下面的示例将多个字符串，以形成一个长字符串连接在一起，然后尝试计算最终的字符串的长度。 此示例演示使用串联运算符时的评估顺序和截断规则。 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+ = &#40;添加分配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;字符串串联 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
