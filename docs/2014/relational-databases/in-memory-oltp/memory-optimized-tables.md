---
title: 内存优化表 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14dddf81-b502-49dc-a6b6-d18b1ae32d2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9123bf89f75fce68a6edd8ba1becd141821fe326
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63158752"
---
# <a name="memory-optimized-tables"></a>内存优化表
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存中 OLTP 通过高效的内存优化的数据访问、对业务逻辑的本机编译以及锁和闩锁免费算法，帮助提高 OLTP 应用程序的性能。 内存中 OLTP 功能包括内存优化表和表类型，以及用于高效访问这些表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程的本机编译。  
  
 有关内存优化表的详细信息，请参阅：  
  
-   [内存优化表简介](memory-optimized-tables.md)  
  
     详细介绍内存优化表的概念，并提供有关数据持久性、访问内存优化表中的数据以及性能和可伸缩性的信息。  
  
-   [表和存储过程的本机编译](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
     详细介绍内存优化表和本机编译的存储过程如何编译为 DLL，并提供相关的安全注意事项。  
  
-   [更改内存优化表](altering-memory-optimized-tables.md)  
  
     内存优化表更新准则（包括更改表列、索引和 bucket_count）。  
  
-   [了解内存优化表的事务](../../database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
     本节提供有关在内存优化表上执行事务的若干主题，其中包括事务隔离级别和交叉容器事务。  
  
-   [用于对内存优化表进行分区的应用程序模式](application-pattern-for-partitioning-memory-optimized-tables.md)  
  
     详细的代码示例，演示了如何使用内存优化表来模拟已分区表。  
  
-   [内存优化表的统计信息](statistics-for-memory-optimized-tables.md)  
  
     详细介绍如何为内存优化表编译统计信息，以及如何维护和手动更新内存优化表的统计信息。  
  
-   [排序规则和代码页](../../database-engine/collations-and-code-pages.md)  
  
     详细介绍对内存优化表支持的排序规则和代码页的限制。  
  
-   [内存优化表中的表和行大小](table-and-row-size-in-memory-optimized-tables.md)  
  
     详细介绍对内存优化表行的 8060 字节限制，并提供表和行大小计算的示例。  
  
-   [内存优化表查询处理指南](a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
     简单介绍针对内存优化表和本机编译的存储过程的查询处理。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](in-memory-oltp-in-memory-optimization.md)  
  
  
