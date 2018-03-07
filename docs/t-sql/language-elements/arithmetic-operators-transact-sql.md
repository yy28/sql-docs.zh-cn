---
title: "算术运算符 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce9ae44451b4307b2fa3e0668467ebe1358f7eaf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="arithmetic-operators-transact-sql"></a>算术运算符 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  算术运算符对两个表达式执行数学运算，这两个表达式可以是数值数据类型类别的一个或多个数据类型。 有关数据类型类别的详细信息，请参阅[TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|运算符|含义|  
|--------------|-------------|  
|[+（加）](../../t-sql/language-elements/add-transact-sql.md)|加|  
|[-（减）](../../t-sql/language-elements/subtract-transact-sql.md)|减法|  
|[*（乘）](../../t-sql/language-elements/multiply-transact-sql.md)|乘|  
|[/ (Divide)](../../t-sql/language-elements/divide-transact-sql.md)|除|  
|[%（取模）](../../t-sql/language-elements/modulo-transact-sql.md)|返回一个除法运算的整数余数。 例如，12 % 5 = 2，这是因为 12 除以 5，余数为 2。|  
  
 加号 （+） 和减号 （-） 运算符还可用来执行算术运算上**datetime**和**smalldatetime**值。  
  
 有关的精度和小数位数的算术运算的结果的详细信息，请参阅[精度、 小数位数和长度 &#40;Transact SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [数学函数 &#40;Transact SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
