---
title: "|（位或）(Transact SQL) |Microsoft 文档"
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
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs: TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5e77a2e7132b7d32a27b7f5be236d75576cb0fcf
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="-bitwise-or-transact-sql"></a>|（位或）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中，将两个指定的整数值转换为二进制表达式后执行逻辑位或运算。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)整数数据类型类别或**位**，**二进制**，或**varbinary**数据类型。 *表达式*视为的按位运算一个二进制数字。  
  
> [!NOTE]  
>  只有一个*表达式*可以是下列任一工具的**二进制**或**varbinary**按位运算中的数据类型。  
  
## <a name="result-types"></a>结果类型  
 返回**int**如果输入的值为**int**、 **smallint**如果输入的值为**smallint**，或**tinyint**如果输入的值为**tinyint**。  
  
## <a name="remarks"></a>注释  
 位运算符 | 取两个表达式的每个对应位，在两个表达式之间执行逻辑位或运算。 如果在输入表达式中有一个位为 1 或两个位均为 1（对于正在解析的当前位），那么结果中的位将被设置为 1；如果输入表达式中的两个位都不为 1，则结果中的位将被设置为 0。  
  
 如果左侧和右侧表达式具有不同的整数数据类型 (例如，左侧*表达式*是**smallint**和右*表达式*是**int**)，较小的数据类型的自变量转换为更大的数据类型。 在此示例中，**smallint * * * 表达式*转换为**int**。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个表，其中**int**数据类型显示的原始值和将表放入一行。  
  
```sql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 以下查询对执行按位或**a_int_value**和**b_int_value**列。  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 二进制表示形式 170 (**a_int_value**或`A`下面) 为`0000 0000 1010 1010`。 二进制表示形式 75 (**b_int_value**或`B`下面) 为`0000 0000 0100 1011`。 对这两个值执行位或运算产生的二进制结果为 `0000 0000 1110 1011`，即十进制数 235。  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>另请参阅  
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124; = &#40;按位 OR 赋值 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [复合运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


