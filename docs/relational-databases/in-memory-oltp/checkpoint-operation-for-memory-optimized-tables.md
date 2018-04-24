---
title: 内存优化表的检查点操作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 838fd0f3b73d2cadb8a9eb42c3e67fb42260b987
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>内存优化表的检查点操作
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  数据和差异文件中内存优化的数据需要定期出现检查点以前移事务日志的活动部分。 通过检查点，内存优化表可还原或恢复到上一个成功的检查点，然后应用事务日志的活动部分以更新内存优化表从而完成恢复。 针对基于磁盘的表和内存优化表的检查点操作是完全不同的操作。 下面介绍不同的场景以及基于磁盘的表和内存优化表的检查点行为：  
  
## <a name="manual-checkpoint"></a>手动检查点  
 发出手动检查点时，它关闭基于磁盘的表和内存优化表的检查点。 即使仅填充了活动数据文件的一部分，也将关闭该文件。  
  
## <a name="automatic-checkpoint"></a>自动检查点  
 对于基于磁盘的表和内存优化表而言，由于保留数据的方式不同，因此自动检查点的实现方式是不同的。  
  
 对于基于磁盘的表，将基于恢复间隔配置选项执行自动检查点（有关详细信息，请参阅[更改数据库的目标恢复时间 (SQL Server)](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)）。  
  
 对于内存优化表，在上次检查点后事务日志文件变得大于 1.5 GB 时，执行自动检查点。 此 1.5 GB 大小包括基于磁盘的表和内存优化表的事务日志记录。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化的对象的存储](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
