---
title: "sql_variant (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4eb946d5b6ed5a9c6d33789166327bd2dd25d7c1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

一种数据类型，用于存储 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的各种数据类型的值。
  
**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>注释  
**sql_variant**可在列、 参数、 变量和用户定义函数的返回值。 **sql_variant**使这些数据库对象以支持其他数据类型的值。
  
类型的列**sql_variant**可能包含不同数据类型的行。 例如，定义为一列**sql_variant**可以存储**int**，**二进制**，和**char**值。
  
**sql_variant**可以 8016 字节的最大长度。 这包括基类型信息和基类型值。 实际基类型值的最大长度是 8,000 个字节。
  
A **sql_variant**数据类型必须首先转换为它的基数据类型值参与等加法和减法操作之前。
  
**sql_variant**可以分配默认值。 该数据类型还可以将 NULL 作为其基础值，但是 NULL 值没有关联的基类型。 此外， **sql_variant**不能有另一个**sql_variant**为其基类型。
  
唯一、 主键或外键可能包含类型的列**sql_variant**，但构成的特定行键的数据值的总长度不应为多个索引的最大长度。 该最大长度是 900 个字节。
  
一个表可以有任意数量的**sql_variant**列。
  
**sql_variant**不能在 CONTAINSTABLE 和 FREETEXTTABLE。
  
ODBC 不完全支持**sql_variant**。 因此，查询的**sql_variant**列返回为二进制数据，当你使用 Microsoft OLE DB 提供程序的 ODBC （msdasql） 一起使用。 例如， **sql_variant**作为 0x505332303931 返回包含字符字符串数据 PS2091 的列。
  
## <a name="comparing-sqlvariant-values"></a>比较 sql_variant 值  
**Sql_variant**数据类型属于转换数据类型层次结构列表的顶部。 有关**sql_variant**比较，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型层次结构顺序分组到数据类型系列。
  
|数据类型层次结构|数据类型系列|  
|---|---|
|**sql_variant**|**sql_variant**|  
|**datetime2**|日期和时间|  
|**datetimeoffset**|日期和时间|  
|**datetime**|日期和时间|  
|**smalldatetime**|日期和时间|  
|**date**|日期和时间|  
|**time**|日期和时间|  
|**float**|近似数值|  
|**real**|近似数值|  
|**decimal**|精确数值|  
|**money**|精确数值|  
|**smallmoney**|精确数值|  
|**bigint**|精确数值|  
|**int**|精确数值|  
|**int**|精确数值|  
|**tinyint**|精确数值|  
|**bit**|精确数值|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|二进制|  
|**binary**|二进制|  
|**uniqueidentifier**|**Uniqueidentifier**|  
  
以下规则适用于**sql_variant**比较：
-   当**sql_variant**比较不同的基数据类型的值和位于不同的数据类型系列的基本数据类型，其数据类型系列较高层次结构图表中的值被视为两个值的更高版本。  
-   当**sql_variant**比较不同的基数据类型的值和的基本数据类型是相同的数据类型系列中，其基本数据类型层次结构图表中较低的值隐式转换为另一种数据类型和然后进行比较。  
-   当**sql_variant**值**char**， **varchar**， **nchar**，或**nvarchar**数据类型相比，其排序规则首先比较是根据以下条件： LCID、 LCID 版本、 比较标志和排序 id。 其中的每个条件都按所列出的顺序作为整数值进行比较。 如果所有这些条件都相等，则将按照排序规则来比较实际的字符串值。  
  
## <a name="converting-sqlvariant-data"></a>转换 sql_variant 数据  
在处理时**sql_variant**数据类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的对象与其他数据类型间的隐式转换**sql_variant**类型。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持从隐式转换**sql_variant**到具有另一个数据类型的对象的数据。
  
## <a name="restrictions"></a>限制  
下表列出了不能通过使用存储的值的类型**sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**时间戳**)|  
|**sql_variant**|**地理**|  
|**hierarchyid**|**geometry**|  
|用户定义类型|**datetimeoffset**|  
  
## <a name="see-also"></a>另请参阅
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  

