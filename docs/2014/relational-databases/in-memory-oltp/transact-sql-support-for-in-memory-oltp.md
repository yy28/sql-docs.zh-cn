---
title: Transact-SQL 对内存中 OLTP 的支持 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8042534c8b22863c5a00abf4969bdb9754cef892
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702215"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>对内存中 OLTP 的 Transact-SQL 支持
  可以使用任何 Transact-SQL 查询或 DML 语句（SELECT、INSERT、UPDATE 或 DELETE）、即席语句和 SQL 模块（如存储过程、表值函数、标量函数、触发器和视图）来访问内存优化表。 有关详细信息，请参阅[使用解释型 Transact-sql 访问内存优化表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)。  
  
 仅引用内存优化表的存储过程可本机编译为机器代码，所提高的性能通常比解释型（基于磁盘的）存储过程更显著。 对于内存优化表的优化访问，使用本机编译存储过程。 有关详细信息，请参阅[本机编译的存储过程](natively-compiled-stored-procedures.md)。  
  
 创建和修改数据对象（DDL 语句）时，修改了以下语句：  
  
-   [更改数据库文件和文件组选项 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) （请参阅 `MEMORY_OPTIMIZED_DATA` ）  
  
-   [SQL Server transact-sql&#41;创建数据库 &#40;](/sql/t-sql/statements/create-database-sql-server-transact-sql) （请参阅 `MEMORY_OPTIMIZED_DATA` ）  
  
-   [&#40;transact-sql&#41;创建过程](/sql/t-sql/statements/create-procedure-transact-sql)（请参阅 `NATIVE_COMPILATION` 、、 `SCHEMABINDING` `EXECUTE AS` 和 `BEGIN ATOMIC` ）  
  
-   [&#40;transact-sql&#41;CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) （请参阅、、、 `MEMORY_OPTIMIZED` `DURABILITY` `BUCKET_COUNT` `INDEX` 和 `HASH` ）  
  
-   [CREATE TYPE &#40;transact-sql&#41;](/sql/t-sql/statements/create-type-transact-sql) （请参阅 `MEMORY_OPTIMIZED` 、、 `BUCKET_COUNT` `INDEX` 和 `HASH` ）  
  
-   [声明 @local_variable &#40;transact-sql&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql) （请参阅 `NULL`  |  `NOT NULL` ）  
  
 内存优化表支持 `PRIMARY KEY` 和 `NOT NULL` 约束。 有关实现不受支持的约束的信息，请参阅[迁移 Check 和 Foreign Key 约束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。  
  
 有关不支持的功能的信息，请参阅[内存中 OLTP 不支持的 Transact-SQL 构造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [支持的数据类型](supported-data-types-for-in-memory-oltp.md)  
  
-   [使用解释型 Transact-SQL 访问内存优化表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [系统视图、存储过程、内存中 OLTP 的 DMV 和等待类型](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP &#40;内存中优化&#41;](in-memory-oltp-in-memory-optimization.md)   
 [本机编译存储过程的迁移问题](migration-issues-for-natively-compiled-stored-procedures.md)   
 [支持的 SQL Server 功能](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  
