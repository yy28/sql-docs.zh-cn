---
title: 本机编译的存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 377aa0cd89ad794bb9efb3744cbf62723512d12c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148708"
---
# <a name="natively-compiled-stored-procedures"></a>本机编译的存储过程
  本机编译的存储过程是编译为访问内存优化表的本机代码的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程。 利用本机编译的存储过程，可在存储过程中高效执行查询和业务逻辑。 有关本机编译过程的更详细信息，请参阅 [Native Compilation of Tables and Stored Procedures](native-compilation-of-tables-and-stored-procedures.md)。 有关将基于磁盘的存储过程迁移到本机编译的存储过程的详细信息，请参阅 [本机编译的存储过程的迁移问题](migration-issues-for-natively-compiled-stored-procedures.md)。  
  
> [!NOTE]  
>  解释型（基于磁盘的）存储过程与本机编译的存储过程之间的一个区别在于解释型存储过程是在首次执行时编译的，而本机编译的存储过程是在创建时编译的。 对于本机编译的存储过程，可在创建时检测到许多错误情况（算术溢出、类型转换和一些被零除情况），并且将导致本机编译的存储过程的创建失败。 对于解释型存储过程，在创建存储过程时这些错误情况通常将不会导致失败，但所有执行都将失败。  
  
 本节主题：  
  
-   [创建本机编译的存储过程](creating-natively-compiled-stored-procedures.md)  
  
-   [原子块](atomic-blocks-in-native-procedures.md)  
  
-   [本机编译的存储过程中支持的构造](supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [在本机编译的存储过程中使用 Try..Catch](../../database-engine/using-try-catch-in-natively-compiled-stored-procedures.md)  
  
-   [本机编译的存储过程支持的构造](supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [本机编译存储过程和执行的 Set 选项](natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [调用本机编译存储过程的最佳做法](best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [监视本机编译的存储过程的执行](monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [从数据访问应用程序调用本机编译的存储过程](calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>请参阅  
 [内存优化表](memory-optimized-tables.md)  
  
  
