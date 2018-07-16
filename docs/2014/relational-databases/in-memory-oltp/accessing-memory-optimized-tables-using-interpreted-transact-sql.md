---
title: 使用解释型 Transact-SQL 访问内存优化表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afcc00e0f6bcc3341f7aafc23aeddfee5e8e8dff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170758"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>使用解释型 Transact-SQL 访问内存优化表
  除了少数例外情况，可以使用任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询或 DML 操作（SELECT、INSERT、UPDATE 或 DELETE）、即席批处理和 SQL 模块（如存储过程、表值函数、触发器和视图）来访问内存优化表。  
  
 解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理或是非本机编译的存储过程的存储过程。 对内存优化表的解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问称为互操作访问。  
  
 内存优化表还可使用本机编译的存储过程访问。 建议将本机编译的存储过程用于对性能至关重要的 OLTP 操作。  
  
 建议将解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问用于以下情况：  
  
-   即席查询和管理任务。  
  
-   报表查询，通常使用本机编译的存储过程中不可用的构造（如窗口函数)。  
  
-   要将应用程序中对性能至关重要的部分迁移到内存优化表，只需极少的应用程序代码更改（或无需更改）。 通过迁移表可能会提高性能。 如果随后将存储过程迁移到本机编译的存储过程，则可以进一步提高性能。  
  
-   当 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句不可用于本机编译的存储过程时。  
  
 访问内存优化表中的数据的解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程中不支持以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 构造。  
  
|区域|不支持|  
|----------|-----------------|  
|访问表|TRUNCATE TABLE<br /><br /> MERGE（使用内存优化的表作为目标）<br /><br /> 动态和键集游标（这些会自动降级为静态）。<br /><br /> 使用上下文连接从 CLR 模块访问。<br /><br /> 从索引视图引用内存优化表。|  
|跨数据库|跨数据库查询<br /><br /> 跨数据库事务<br /><br /> 链接服务器|  
  
## <a name="table-hints"></a>表提示  
 有关表提示的详细信息，请参阅。 [表提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-table)。 添加了 SNAPSHOT 隔离来支持 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]。  
  
 使用解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)]访问内存优化表时，不支持以下表提示。  
  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *integer*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  
 当使用解释型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 从显式或隐式事务访问内存优化表时，必须包含隔离级别表提示（如 SNAPSHOT、REPEATABLEREAD 或 SERIALIZABLE），也可以使用 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT。 有关详细信息，请参阅[具有内存优化表的事务隔离级别准则](memory-optimized-tables.md)并[ALTER DATABASE SET 选项&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
> [!NOTE]  
>  由在自动提交模式下运行的查询访问的内存优化表不需要隔离级别表提示。  
  
## <a name="see-also"></a>请参阅  
 [对内存中 OLTP 的 Transact-SQL 支持](transact-sql-support-for-in-memory-oltp.md)   
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
