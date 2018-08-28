---
title: 内存中 OLTP 支持的数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 20c3f2a234e856c5da2095f8fefd1b09b22a6331
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058639"
---
# <a name="supported-data-types-for-in-memory-oltp"></a>内存中 OLTP 支持的数据类型
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本文列出了内存中 OLTP 功能不支持的数据类型：  
  
-   内存优化表  
  
-   本机编译的 T-SQL 模块  
  
## <a name="unsupported-data-types"></a>不支持的数据类型  
 不支持以下数据类型：  
  
||||  
|-|-|-|  
|[datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography (Transact-SQL)](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry (Transact-SQL)](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion (Transact-SQL)](../../t-sql/data-types/rowversion-transact-sql.md)|[xml (Transact-SQL)](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant (Transact-SQL)](../../t-sql/data-types/sql-variant-transact-sql.md)|用户定义类型|实例时都提供 SQL Server 登录名。|  
  
## <a name="notable-supported-data-types"></a>值得注意的受支持数据类型  
 内存中 OLTP 的功能支持大多数数据类型。 以下几个数据类型值得注意：  
  
|字符串和二进制类型|有关详细信息，请参阅：|  
|-----------------------------|--------------------------|  
|binary 和 varbinary*|[binary 和 varbinary (Transact-SQL)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char 和 varchar*|[char 和 varchar (Transact-SQL)](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar 和 nvarchar*|[nchar 和 nvarchar (Transact-SQL)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
对于上述字符串和二进制数据类型，从 SQL Server 2016 开始：  
  
- 单个内存优化表还可以具有多个长列（如 `nvarchar(4000)`），即使其长度之和大于物理行大小（即 8060 字节）也没有关系。  
  
- 内存优化表可以具有数据类型的最长字符串和二进制列，例如 `varchar(max)`。  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>标识 LOB 和其他行外列

自 SQL Server 2016 起，内存优化表[支持行外列](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)，即允许一个表行大于 8060 个字节。 以下 Transact-SQL SELECT 语句报告了内存优化表中的所有行外列。 注意：

- 所有索引键列均存储于行内。
  - 现在，允许在内存优化表上的非唯一索引键中包含可为 NULL 的列。
  - 可以在内存优化表上将索引声明为 UNIQUE。
- 所有 LOB 列存储在行外。
- -1 的 max_length 表示大型对象 (LOB) 列。


```sql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


### <a name="other-data-types"></a>其他数据类型


|其他类型|有关详细信息，请参阅：|  
|-----------------|--------------------------|  
|表类型|[内存优化表变量](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)|  
  
## <a name="see-also"></a>另请参阅  
 [对内存中 OLTP 的 Transact-SQL 支持](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [在内存优化的表中实现 SQL_VARIANT](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
 [内存优化表中的表和行大小](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
