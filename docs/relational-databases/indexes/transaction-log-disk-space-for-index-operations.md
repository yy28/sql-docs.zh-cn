---
title: 索引操作的事务日志磁盘空间 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4af90d16e4e81b5d2ee1dc73de78826073d1cbff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909465"
---
# <a name="transaction-log-disk-space-for-index-operations"></a>索引操作的事务日志磁盘空间
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  大规模索引操作可以产生大量数据负载，从而导致事务日志的空间很快被占满。 若要确保索引操作能够回滚，不能在完成索引操作之前截断事务日志，但可以在索引操作期间备份日志。 因此，事务日志必须具有足够的空间，以存储索引操作期间的索引操作事务和任何并发用户事务。 这对脱机索引操作和联机索引操作都适用。 因为在脱机索引操作期间不能访问基础表，所以用户事务可能很少，日志的增长速度不快。 联机索引操作不能防止并发用户活动，因此，大规模联机索引操作与大量的并发用户事务相结合可能会导致事务日志不断增长，而不会提供截断日志的选项。  
  
## <a name="recommendations"></a>建议  
 运行大规模索引操作时，请考虑下列建议：  
  
1.  确保在联机运行大规模索引操作之前备份并截断事务日志，并且日志中具有足够的空间来存储计划的索引事务和用户事务。  
  
2.  考虑将索引操作的 SORT_IN_TEMPDB 选项设置为 ON。 这将把索引事务与并发用户事务分开。 索引事务将存储在 **tempdb** 事务日志中，而并发用户事务将存储在用户数据库的事务日志中。 这允许在索引操作期间截断用户数据库中的事务日志（如果需要）。 此外，如果 **tempdb** 日志与用户数据库日志不在同一磁盘上，两个日志将不会争用同一磁盘空间。  
  
    > [!NOTE]  
    >  验证 **tempdb** 数据库和事务日志具有足够的空间来处理索引操作。 不能在索引操作完成之前截断 **tempdb** 事务日志。  
  
3.  使用数据库恢复模型，它允许对索引操作做最小的日志记录。 这可以减少日志的大小，并防止日志占满日志空间。  
  
4.  不要在显式事务中执行联机索引操作。 在显式事务结束之前不会截断日志。  
  
## <a name="related-content"></a>相关内容  
 [索引 DDL 操作的磁盘空间要求](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [索引磁盘空间示例](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
