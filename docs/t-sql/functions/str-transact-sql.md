---
title: "STR (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7cddf1af7eba56824e41ad1ebaedb9aecdc37074
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回由数字数据转换来的字符数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *float_expression*  
 近似数值的表达式 (**float**) 带小数点的数据类型。  
  
 *length*  
 总长度。 它包括小数点、符号、数字以及空格。 默认值为 10。  
  
 *decimal*  
 是右侧的位数。 *十进制*必须小于或等于 16。 如果*十进制*为多个 16，然后将结果截断至小数点右侧的十六个位置。  
  
## <a name="return-types"></a>返回类型  
 **varchar**  
  
## <a name="remarks"></a>注释  
 如果提供的值*长度*和*十进制*STR 参数应为正数。 在默认情况下或小数参数为 0 时，数字舍入为整数。 指定的长度应大于或等于小数点前面的部分加上数字符号（如果有）的长度。 Short *float_expression*是指定的长度和 long 类型的值中的右对齐*float_expression*截断到指定的小数位数。 例如，STR (12**，**10) 产生结果为 12。 这在结果集中右对齐。 但是，STR (1223年**，**2) 将截断的结果集 * *。 可以嵌套字符串函数。  
  
> [!NOTE]  
>  若要将转换为 Unicode 数据，使用转换内的 STR 或[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)转换函数。  
  
## <a name="examples"></a>示例  
 以下示例将由五个数字和一个小数点组成的表达式转换为有六个位置的字符串。 数字的小数部分舍入为一个小数位。  
  
```  
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 当表达式超出指定长度时，字符串为指定长度返回 `**`。  
  
```  
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 即使数字数据嵌套在 `STR` 内，结果也是带指定格式的字符数据。  
  
```  
SELECT STR (FLOOR (123.45), 8, 3;)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


