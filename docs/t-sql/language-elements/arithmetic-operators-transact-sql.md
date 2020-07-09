---
title: 算术运算符 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6fd33150c41b692c803348f3246a165b785f0a1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85990603"
---
# <a name="arithmetic-operators-transact-sql"></a>算术运算符 (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

算术运算符对使用一个或多个数据类型的两个表达式运行数学运算。 它们从数值数据类型类别运行。 有关数据类型类别的详细信息，请参阅 [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|操作员|含义|  
|--------------|-------------|  
|[+（加）](../../t-sql/language-elements/add-transact-sql.md)|加|  
|[-（减）](../../t-sql/language-elements/subtract-transact-sql.md)|减|  
|[*（乘）](../../t-sql/language-elements/multiply-transact-sql.md)|乘|  
|[/ (Divide)](../../t-sql/language-elements/divide-transact-sql.md)|除|  
|[%（取模）](../../t-sql/language-elements/modulo-transact-sql.md)|返回一个除法运算的整数余数。 例如，12 % 5 = 2，这是因为 12 除以 5，余数为 2。|  
  
加 (+) 和减 (-) 运算符也可用于对 datetime  和 smalldatetime  值运行算术运算。  
  
若要详细了解算术运算结果的精度和确定位数，请参阅[精度、确定位数和长度 &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
[数学函数 (Transact-SQL)](../../t-sql/functions/mathematical-functions-transact-sql.md)   
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
