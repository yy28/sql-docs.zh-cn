---
title: 数据类型 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 9/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c22a3218cf55ff934a0b74abd6e21dbb9012231e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-types-transact-sql"></a>数据类型 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，每个列、局部变量、表达式和参数都具有一个相关的数据类型。 数据类型是一种属性，用于指定对象可保存的数据的类型：整数数据、字符数据、货币数据、日期和时间数据、二进制字符串等。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供系统数据类型集，该类型集定义了可与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起使用的所有数据类型。 还可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 定义自己的数据类型。 别名数据类型基于系统提供的数据类型。 有关别名数据类型的详细信息，请参阅 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)。 用户定义类型从您使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 支持的编程语言之一创建的类的方法和运算符中获取它们的特征。
  
当两个具有不同数据类型、排序规则、精度、小数位数或长度的表达式通过运算符进行组合时，结果的特征由以下规则确定：
-   结果的数据类型是通过将数据类型的优先顺序规则应用到输入表达式的数据类型来确定的。 有关详细信息，请参阅[数据类型优先级 (Transact-SQL)](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
-   当结果数据类型为 char、varchar、text、nchar、nvarchar 或 ntext 时，结果的排序规则由排序规则的优先顺序规则确定。 有关详细信息，请参阅[排序规则优先顺序 (Transact-SQL)](../../t-sql/statements/collation-precedence-transact-sql.md)。  
-   结果的精度、小数位数及长度取决于输入表达式的精度、小数位数及长度。 有关详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了数据类型同义词，以便实现 ISO 兼容性。 有关详细信息，请参阅[数据类型同义词 (Transact-SQL)](../../t-sql/data-types/data-type-synonyms-transact-sql.md)。
  
## <a name="data-type-categories"></a>数据类型类别
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据类型归纳为下列类别：
  
|||  
|-|-|  
|精确数字|Unicode 字符串|  
|近似数字|二进制字符串|  
|日期和时间|其他数据类型|  
|字符串||  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，根据其存储特征，某些数据类型被指定为属于下列各组：
-   大值数据类型：varchar(max) 和 nvarchar(max)  
-   大型对象数据类型：text、ntext、image、varbinary(max) 和 xml  
  
    > [!NOTE]  
    >  sp_help 返回 -1 作为较大值数据类型和 xml 数据类型的长度。  
  
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
|[空间几何类型](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) |[空间地理类型](../../t-sql/spatial-geography/spatial-types-geography.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md) | |
  
## <a name="see-also"></a>另请参阅
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)  
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[函数 (Transact-SQL)](../../t-sql/functions/functions.md)  
[LIKE (Transact-SQL)](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  
