---
title: "数据类型 (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 9/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 75efc7b5a58b3739a196e36b2c80d4ee37a92003
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---

# <a name="data-types-transact-sql"></a>数据类型 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，每个列、局部变量、表达式和参数都具有一个相关的数据类型。 数据类型是一种属性，用于指定对象可保存的数据的类型：整数数据、字符数据、货币数据、日期和时间数据、二进制字符串等。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供系统数据类型集，该类型集定义了可与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起使用的所有数据类型。 你还可以定义自己的数据类型中[!INCLUDE[tsql](../../includes/tsql-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 别名数据类型基于系统提供的数据类型。 有关别名数据类型的详细信息，请参阅[CREATE TYPE &#40;Transact SQL &#41;](../../t-sql/statements/create-type-transact-sql.md). 用户定义类型从您使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 支持的编程语言之一创建的类的方法和运算符中获取它们的特征。
  
当两个具有不同数据类型、排序规则、精度、小数位数或长度的表达式通过运算符进行组合时，结果的特征由以下规则确定：
-   结果的数据类型是通过将数据类型的优先顺序规则应用到输入表达式的数据类型来确定的。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
-   结果数据类型时，由排序规则优先顺序规则确定的结果的排序规则**char**， **varchar**，**文本**， **nchar**， **nvarchar**，或**ntext**。 有关详细信息，请参阅[排序规则优先顺序 &#40;Transact SQL &#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   结果的精度、小数位数及长度取决于输入表达式的精度、小数位数及长度。 有关详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为 ISO 兼容性提供数据类型的同义词。 有关详细信息，请参阅[数据类型同义词 &#40;Transact SQL &#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>数据类型类别
中的数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]分为以下类别：
  
|||  
|-|-|  
|精确数字|Unicode 字符串|  
|近似数字|二进制字符串|  
|日期和时间|其他数据类型|  
|字符串||  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，根据其存储特征，某些数据类型被指定为属于下列各组：
-   大型值数据类型： **varchar （max)**，和**nvarchar (max)**  
-   大型对象数据类型：**文本**， **ntext**，**映像**， **varbinary （max)**，和**xml**  
  
    > [!NOTE]  
    >  sp_help 返回-1 作为最大值的长度和**xml**数据类型。  
  
### <a name="exact-numerics"></a>精确数字
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>近似数字
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>日期和时间
  
|||  
|-|-|  
|[date](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[time](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>字符串
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>Unicode 字符串
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>二进制字符串
  
|||  
|-|-|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>其他数据类型
  
|||  
|-|-|  
|[cursor](../../t-sql/data-types/cursor-transact-sql.md)|[rowversion](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[空间 Geometry 类型](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[空间 Geography 类型](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>另请参阅
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[声明@local_variable&#40;Transact SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
[执行 &#40;Transact SQL &#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[函数 &#40;Transact SQL &#41;](../../t-sql/functions/functions.md)  
[如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  

