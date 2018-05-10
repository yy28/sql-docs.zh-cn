---
title: 内存中 OLTP（内存中优化）| Microsoft Docs
ms.custom: ''
ms.date: 11/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
caps.latest.revision: 106
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b9843ce1aedeb297e1960569a73f013678085511
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="in-memory-oltp-in-memory-optimization"></a>内存中 OLTP（内存中优化）
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 可显著改善事务处理、数据引入和数据加载的性能以及暂时数据方案。  若要跳转到快速测试自己的内存优化表和本机编译的存储过程所需的基本代码和知识，请参阅
 -  [快速入门 1：可提高 Transact SQL 性能的内存中 OLTP 技术](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)。  
 
说明内存中 OLTP 并演示性能优势的 17 分钟视频：

-  [In-Memory OLTP in SQL Server 2016](https://www.youtube.com/watch?v=l5l5eophmK4)（SQL Server 2016 中的内存中 OLTP）。

下载视频中所用的内存中 OLTP 的性能演示： 

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

深入了解内存中 OLTP 的详细概述以及查看显示技术中性能优势的方案：

- [概述和使用方案](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 请注意， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 是用于提高事务处理性能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术。 有关提高报告和分析查询性能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术，请参阅 [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)。
  
 已对 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]，以及 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的内存中 OLTP 进行了多项改进。 增加了 Transact-SQL 外围应用，以使其更易于迁移数据库应用程序。 添加了对内存优化表和本机编译的存储过程执行 ALTER 操作的支持，以使其更易于维护应用程序。 有关 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 中新增功能的信息，请参阅[列存储索引 - 新增功能](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)。  
  
> [!NOTE]  
>  **进行试用**  
>   
>  内存中 OLTP 在高级层和业务关键层 Azure SQL 数据库和弹性池中可用。 若要在 Azure SQL 数据库中开始使用内存中 OLTP 以及列存储，请参阅 [Optimize Performance using In-Memory Technologies in SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/)（在 SQL 数据库中使用内存中技术优化性能）。  
  

## <a name="in-this-section"></a>在本节中  
 本节包括下列主题：  
  
|主题|Description|  
|-----------|-----------------|  
|[快速入门 1：可提高 Transact SQL 性能的内存中 OLTP 技术](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|深入探讨内存中 OLTP|
|[概述和使用方案](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|有关什么是内存中 OLTP 以及什么是显示性能优势的方案的概述。|
|[使用内存优化表的要求](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|讨论使用内存优化的表的硬件和软件要求及指导原则。|  
|[内存中 OLTP 代码示例](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|包含说明如何创建和使用内存优化的表的代码示例。|  
|[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|介绍内存优化的表。|  
|[内存优化表变量](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|一个代码示例，其中展示如何使用内存优化的表变量代替传统的表变量以减少 tempdb 的使用次数。|  
|[内存优化表上的索引](http://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|介绍内存优化索引。|  
|[本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|介绍本机编译的存储过程。|  
|[管理内存中 OLTP 的内存](http://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|了解和管理系统中的内存用量。|  
|[创建和管理用于内存优化对象的存储](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|论述数据和差异文件，其中存储有关内存优化的表中事务的信息。|  
|[内存优化表的备份、还原和恢复](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|讨论内存优化表的备份、还原和恢复。|  
|[对内存中 OLTP 的 Transact-SQL 支持](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|讨论 [!INCLUDE[tsql](../../includes/tsql-md.md)] 对 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]的支持。|  
|[对内存中 OLTP 数据库的高可用性支持](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|讨论 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]中的可用性组和故障转移群集。|  
|[对内存中 OLTP 的 SQL Server 支持](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|列出支持内存优化表的新增和更新的语法和功能。|  
|[迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|论述如何将基于磁盘的表迁移到内存优化的表。|  
  
 有关 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 的详细信息，请参阅：  

- [说明内存中 OLTP 并演示性能优势的视频](https://www.youtube.com/watch?v=l5l5eophmK4)。

- [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [SQL Server 内存中 OLTP 内部组件技术白皮书](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [SQL Server In-Memory OLTP and Columnstore Feature Comparison](http://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   SQL Server 2016 内存中 OLTP 的新增功能 [第 1 部分](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) 和 [第 2 部分](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [内存中 OLTP - 常见的工作负荷模式和迁移注意事项](http://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [内存中 OLTP 博客](http://go.microsoft.com/fwlink/?LinkId=311696)  
  
## <a name="see-also"></a>另请参阅  
 [数据库功能](../../relational-databases/database-features.md)  
  
  
