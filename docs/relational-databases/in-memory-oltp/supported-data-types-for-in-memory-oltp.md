---
title: "内存中 OLTP 支持的数据类型 | Microsoft Docs"
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a928c1f77586198fd0d33cafa445ea406a437c6b
ms.lasthandoff: 04/11/2017

---
# <a name="supported-data-types-for-in-memory-oltp"></a>内存中 OLTP 支持的数据类型
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本文列出了内存中 OLTP 功能不支持的数据类型：  
  
-   内存优化表  
  
-   本机编译的存储过程  
  
## <a name="unsupported-data-types"></a>不支持的数据类型  
 不支持以下数据类型：  
  
||||  
|-|-|-|  
|[datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography (Transact-SQL)](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry (Transact-SQL)](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid (Transact-SQL)](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion (Transact-SQL)](../../t-sql/data-types/rowversion-transact-sql.md)|[xml (Transact-SQL)](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant (Transact-SQL)](../../t-sql/data-types/sql-variant-transact-sql.md)|用户定义类型|。|  
  
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

以下 Transact-SQL SELECT 语句报告了内存优化表中的所有行外列。 注意：

- 所有索引键列均存储于行内。
  - 现在，允许在内存优化表上的非唯一索引键中包含可为 NULL 的列。
  - 可以在内存优化表上将索引声明为 UNIQUE。
- 所有 LOB 列存储在行外。
- -1 的 max_length 表示大型对象 (LOB) 列。


```tsql
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


#### <a name="natively-compiled-modules-support-for-lobs"></a>本机编译模块支持 LOB


在本机编译模块中使用内置字符串函数时（如本机进程），该函数可以接受字符串 LOB 类型。 例如，在本机进程中，LTrim 函数可输入 nvarchar(max) 或 varbinary(max) 类型的参数。

这些 LOB 可以是来自本机编译标量 UDF（用户定义的函数）的返回类型。


### <a name="other-data-types"></a>其他数据类型


|其他类型|有关详细信息，请参阅：|  
|-----------------|--------------------------|  
|表类型|[内存优化表变量](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|  
  
## <a name="see-also"></a>另请参阅  
 [对内存中 OLTP 的 Transact-SQL 支持](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [在内存优化的表中实现 LOB 列](http://msdn.microsoft.com/en-us/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [在内存优化的表中实现 SQL_VARIANT](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  

