---
title: 本机编译的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2ec17857ed97fdc9167b98357d7ae22afbf5dc01
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="natively-compiled-stored-procedures"></a>本机编译的存储过程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本机编译的存储过程是编译为访问内存优化表的本机代码的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。 通过本机编译的存储过程，可在存储过程中高效执行查询和业务逻辑。 有关本机编译过程的更详细信息，请参阅 [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)。 有关将基于磁盘的存储过程迁移到本机编译的存储过程的详细信息，请参阅 [本机编译的存储过程的迁移问题](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)。  
  
> [!NOTE]  
>  解释型（基于磁盘的）存储过程与本机编译的存储过程之间的一个区别在于解释型存储过程是在首次执行时编译的，而本机编译的存储过程是在创建时编译的。 对于本机编译的存储过程，可在创建时检测到许多错误情况（例如算术溢出、类型转换和一些被零除的情况），并且将导致本机编译的存储过程的创建失败。 对于解释型存储过程，在创建存储过程时这些错误情况通常不会导致失败，但所有执行都将失败。  
  
 本节主题：  
  
-   [创建本机编译的存储过程](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [原子块](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)  
  
-   [本机编译的 T-SQL 模块支持的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [对于本机编译的 T-SQL 模块支持的 DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [本机编译存储过程和执行的 Set 选项](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [调用本机编译存储过程的最佳做法](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [监视本机编译的存储过程的执行](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [从数据访问应用程序调用本机编译的存储过程](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
