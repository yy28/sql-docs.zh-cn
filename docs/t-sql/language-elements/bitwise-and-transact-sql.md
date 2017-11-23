---
title: "&amp;（位与）(Transact SQL) |Microsoft 文档"
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
- bitwise
- '&'
- '&_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d249ca1552197a5fb7e53540c40e70c864d134bb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp;（位与）(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在两个整数值之间执行“逻辑位与”运算。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任意整数数据类型类别中，数据类型或**位**，或**二进制**或**varbinary**数据类型。 *表达式*视为的按位运算一个二进制数字。  
  
> [!NOTE]  
>  在按位运算中，只有一个*表达式*可以是下列任一工具的**二进制**或**varbinary**数据类型。  
  
## <a name="result-types"></a>结果类型  
 **int**如果输入的值为**int**。  
  
 **smallint**如果输入的值为**smallint**。  
  
 **tinyint**如果输入的值为**tinyint**或**位**。  
  
## <a name="remarks"></a>注释  
 **&** 按位运算符执行两个表达式，使每个相应位的两个表达式之间的按位逻辑 AND。 当且仅当输入表达式中两个位（正在被解析的当前位）的值都为 1 时，结果中的位才被设置为 1；否则，结果中的位被设置为 0。  
  
 如果左侧和右侧表达式具有不同的整数数据类型 (例如，左侧*表达式*是**smallint**和右*表达式*是**int**)，较小的数据类型的自变量转换为更大的数据类型。 在这种情况下， **smallint***表达式*转换为**int**。  
  
## <a name="examples"></a>示例  
 下面的示例创建表使用**int**数据类型来存储的值，并将两个值插入一行。  
  
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
  
 下面的查询将在 `a_int_value` 和 `b_int_value` 列之间执行位与运算。  
  
```  
SELECT a_int_value & b_int_value  
FROM bitwise;  
GO  
```  
  
 下面是结果集：  
  
```  
-----------   
10            
  
(1 row(s) affected)  
```  
  
 二进制表示形式 170 (`a_int_value`或`A`) 是`0000 0000 1010 1010`。 75（`b_int_value` 或 `B`）的二进制表示形式是 `0000 0000 0100 1011`。 对上述两个值执行“位与”运算将产生二进制结果 `0000 0000 0000 1010`，即十进制数 10。  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [& = &#40;按位与赋值 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


