---
title: 支持的数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de5f805a9d722974adf7975f713436bc7b1ca4d0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63155157"
---
# <a name="supported-data-types"></a>支持的数据类型
  内存优化表和本机编译存储过程中 **支持** 以下数据类型：  
  
 **数值数据类型**  
  
|数据类型|更多信息|  
|---------------|--------------------------|  
|int|[int、bigint、smallint 和 tinyint (Transact-SQL)](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|bigint|[int、bigint、smallint 和 tinyint (Transact-SQL)](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|smallint|[int、bigint、smallint 和 tinyint (Transact-SQL)](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|tinyint|[int、bigint、smallint 和 tinyint (Transact-SQL)](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|decimal|[decimal 和 numeric (Transact-SQL)](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|numeric|[decimal 和 numeric (Transact-SQL)](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|float|[float 和 real (Transact-SQL)](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|real|[float 和 real (Transact-SQL)](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|money|[money 和 smallmoney (Transact-SQL)](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
|smallmoney|[money 和 smallmoney (Transact-SQL)](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
  
 **字符串数据类型**  
  
|数据类型|更多信息|  
|---------------|--------------------------|  
|char(n)|[char 和 varchar (Transact-SQL)](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|varchar （n） <sup>1</sup>|[char 和 varchar (Transact-SQL)](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|nchar(n)|[nchar 和 nvarchar (Transact-SQL)](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|nvarchar （n） <sup>1</sup>|[nchar 和 nvarchar (Transact-SQL)](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|sysname|[nchar 和 nvarchar (Transact-SQL)](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
  
 <sup>1</sup>限制为每行总数8060个字节，可变长度类型中的计数（n）。  
  
 有关支持的排序规则的信息，请参阅 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)。  
  
 **日期和时间数据类型**  
  
|数据类型|更多信息|  
|---------------|--------------------------|  
|date|[date (Transact-SQL)](/sql/t-sql/data-types/date-transact-sql)|  
|time|[time (Transact-SQL)](/sql/t-sql/data-types/time-transact-sql)|  
|日期/时间|[datetime (Transact-SQL)](/sql/t-sql/data-types/datetime-transact-sql)|  
|datetime2|[datetime2 (Transact-SQL)](/sql/t-sql/data-types/datetime2-transact-sql)|  
|smalldatetime|[smalldatetime (Transact-SQL)](/sql/t-sql/data-types/smalldatetime-transact-sql)|  
  
 **二进制数据类型**  
  
|数据类型|更多信息|  
|---------------|--------------------------|  
|bit|[bit (Transact-SQL)](/sql/t-sql/data-types/bit-transact-sql)|  
|binary(n)|[binary 和 varbinary (Transact-SQL)](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
|varbinary （n） <sup>1</sup>|[binary 和 varbinary (Transact-SQL)](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
  
 <sup>1</sup>限制为每行总数8060个字节，可变长度类型中的计数（n）。  
  
 **其他数据类型**  
  
|数据类型|更多信息|  
|---------------|--------------------------|  
|uniqueidentifier|[uniqueidentifier (Transact-SQL)](/sql/t-sql/data-types/uniqueidentifier-transact-sql)|  
  
 **不支持的数据类型**  
  
 不支持以下数据类型：  
  
||||  
|-|-|-|  
|DATETIMEOFFSET|GEOGRAPHY|GEOMETRY|  
|HIERARCHYID|大型对象 (LOB)。 例如，varchar(max)、nvarchar(max)、varbinary(max)、image、xml、text 和 ntext。|ROWVERSION|  
|sql_variant|CLR 函数|用户定义类型 (UDT)|  
  
## <a name="see-also"></a>另请参阅  
 [对内存中 OLTP 的 transact-sql 支持](transact-sql-support-for-in-memory-oltp.md)   
 [在内存优化表中实现 LOB 列](../../database-engine/implementing-lob-columns-in-a-memory-optimized-table.md)   
 [在内存优化的表中实现 SQL_VARIANT](implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  
