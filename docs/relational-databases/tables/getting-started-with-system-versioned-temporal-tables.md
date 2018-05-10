---
title: 系统版本控制临时表入门 | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6ee93c85f02d60c49c9813dc4756699d5bd7df87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>系统版本控制临时表入门
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  根据你的方案，你可以创建新的系统版本控制临时表，或通过将临时属性添加到现有的表架构修改现有的系统版本控制临时表。   
修改临时表中的数据时，系统将生成对应用程序和最终用户透明的版本历史记录。 因此，使用系统版本控制临时表时，不需要对修改表或查询最新（实际）状态的数据的方式进行任何更改。   
除了常规的 DML 和查询，临时表还提供了简单方便的方法来让你通过扩展的 Transact-SQL 语法从数据历史记录中获得见解。   
每个系统版本控制表都分配有一个历史记录表，但该表对用户完全透明，除非他们想要通过创建附加索引或选择不同的存储选项来优化工作负载性能或存储空间。    
下图说明了使用系统版本控制临时表的典型工作流：   
![时态入门](../../relational-databases/tables/media/getting-started-with-temporal.png "Getting Started with Temporal")  
  
 本主题分为以下 5 个子主题：  
  
-   [创建由系统控制版本的临时表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
-   [在系统版本控制的临时表中修改数据](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
-   [在系统版本控制临时表中查询数据](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
-   [更改系统版本控制的临时表架构](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)  
  
-   [停止对系统版本的临时表的系统版本控制](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
## <a name="see-also"></a>另请参阅  
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [临时表系统一致性检查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [临时表分区](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [临时表注意事项和限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [临时表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系统版本控制的临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [临时表元数据视图和函数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
