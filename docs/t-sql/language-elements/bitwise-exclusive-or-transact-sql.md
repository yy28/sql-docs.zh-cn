---
title: "^ (位异或) (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ^_TSQL
- Bitwise Exclusive OR
- Exclusive
- ^
- bitwise
- OR
dev_langs: TSQL
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- OR operator
- exclusive OR mathematical operations
- bitwise exclusive OR (^)
ms.assetid: f38f0ad4-46d0-40ea-9851-0f928fda5293
caps.latest.revision: "44"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4923d20bdeb7e625157a47c0f70e685895c41550
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="-bitwise-exclusive-or-transact-sql"></a>^（位异或）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  执行两个整数值按位异或运算。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression ^ expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何一种数据类型的整数数据类型类别中，或**位**，或**二进制**或**varbinary**数据类型。 *表达式*视为的按位运算一个二进制数字。  
  
> [!NOTE]  
>  只有一个*表达式*可以是下列任一工具的**二进制**或**varbinary**按位运算中的数据类型。  
  
## <a name="result-types"></a>结果类型  
 **int**如果输入的值为**int**。  
  
 **smallint**如果输入的值为**smallint**。  
  
 **tinyint**如果输入的值为**tinyint**。  
  
## <a name="remarks"></a>注释  
 **^** 按位运算符执行逻辑异按位或两个表达式，使每个相应位的两个表达式之间。 如果在输入表达式的正在被解析的对应位中，任意一位（但不是两个位）的值为 1，则结果中该位的值被设置为 1。 如果相对应的两个位的值都为 0 或者都为 1，那么结果中该位的值被清除为 0。  
  
 如果左侧和右侧表达式具有不同的整数数据类型 (例如，左侧*表达式*是**smallint**和右*表达式*是**int**)，较小的数据类型的自变量转换为更大的数据类型。 在这种情况下， **smallint***表达式*转换为**int**。  
  
## <a name="examples"></a>示例  
 下面的示例创建表使用**int**数据类型来存储的原始值，并将两个值插入一行。  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 下面的查询对 `a_int_value` 和 `b_int_value` 列执行位异或运算。  
  
```  
SELECT a_int_value ^ b_int_value  
FROM bitwise;  
GO  
```  
  
 下面是结果集：  
  
```  
-----------   
225           
  
(1 row(s) affected)  
```  
  
 二进制表示形式 170 (`a_int_value`或`A`) 是`0000 0000 1010 1010`。 75（`b_int_value` 或 `B`）的二进制表示形式是 `0000 0000 0100 1011`。 在这两个值之间执行位异或运算所产生的二进制结果是 `0000 0000 1110 0001`，即十进制数 225。  
  
```  
(A ^ B)     
         0000 0000 1010 1010  
         0000 0000 0100 1011  
         -------------------  
         0000 0000 1110 0001  
```  
  

  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^ = &#40;按位异或赋值 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


