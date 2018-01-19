---
title: "~ （位非） (Transact SQL) |Microsoft 文档"
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
- ~_TSQL
- bitwise
- NOT
- ~
- Bitwise NOT
dev_langs: TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
caps.latest.revision: "42"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5bd0f8234088fbb358740d5c9b4e753d9ecaa11d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="-bitwise-not-transact-sql"></a>~（位非）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对整数值执行逻辑位非运算。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>参数  
 *expression*  
 是任何有效[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的任何一种数据类型的整数数据类型类别，**位**，或**二进制**或**varbinary**数据类型。 *表达式*视为的按位运算一个二进制数字。  
  
> [!NOTE]  
>  只有一个*表达式*可以是下列任一工具的**二进制**或**varbinary**按位运算中的数据类型。  
  
## <a name="result-types"></a>结果类型  
 **int**如果输入的值为**int**。  
  
 **smallint**如果输入的值为**smallint**。  
  
 **tinyint**如果输入的值为**tinyint**。  
  
 **位**如果输入的值为**位**。  
  
## <a name="remarks"></a>注释  
  **~** 按位运算符执行按位逻辑不为*表达式*，反过来逐位。 如果*表达式*具有值为 0，结果集中的位将设置为 1; 否则，结果中的位将清值为 0。 换句话说，1 改成 0，而 0 则改成 1。  
  
> [!IMPORTANT]  
>  执行任何种类的位运算时，位运算中使用的表达式的存储长度都是很重要的。 建议您在存储值时使用该相同的字节数。 例如，存储十进制值为 5 作为**tinyint**， **smallint**，或**int**产生存储具有不同数量的字节的值： **tinyint**使用 1 个字节; 存储数据**smallint**使用 2 个字节，存储数据和**int**使用 4 个字节存储数据。 因此，对执行按位运算**int**十进制值会产生不同结果与使用直接的二进制或十六进制的转换，尤其是当 **~**  (位非） 使用运算符。 位非运算可能针对长度较短的变量执行。 这种情况下，当长度较短的变量转换为较长的数据类型变量时，上 8 位中的位将不能设置为期望的值。 我们建议先将较小的数据类型变量转换为较大的数据类型，然后对结果执行非运算。  
  
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
  
 以下查询对 `a_int_value` 和 `b_int_value` 列执行位非运算。  
  
```  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 下面是结果集：  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 二进制表示形式 170 (`a_int_value`或`A`) 是`0000 0000 1010 1010`。 对这个值执行“位非”运算将产生二进制结果 `1111 1111 0101 0101`，即十进制数 -171。 75 的二进制表示形式是 `0000 0000 0100 1011`。 执行位非运算将生成 `1111 1111 1011 0100`，该结果等于十进制 -76。  
  
```  
 (~A)     
         0000 0000 1010 1010  
         -------------------  
         1111 1111 0101 0101  
(~B)     
         0000 0000 0100 1011  
         -------------------  
         1111 1111 1011 0100  
```  
  
 
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [按位运算符 &#40;Transact SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


