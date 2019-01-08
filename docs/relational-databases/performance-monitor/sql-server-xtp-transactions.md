---
title: SQL Server XTP 事务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: f56c3a7a7d5a03ed4253c8a63df37eb5e7b26d8d
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380808"
---
# <a name="sql-server-xtp-transactions"></a>SQL Server XTP 事务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 事务性能对象包括有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中涉及内存中 OLTP 事务的计数器。  
  
 下表说明了 **SQL Server XTP 事务** 计数器。  
  
|计数器|描述|  
|-------------|-----------------|  
|**级联中止数/秒**|由于提交依赖关系回滚而每秒回滚的事务数（平均值）。|  
|**采用的提交依赖关系数/秒**|事务每秒采用的提交依赖关系数（平均值）。|  
|**准备好的只读事务数/秒**|准备好进行提交处理的每秒只读事务数。|  
|**保存点刷新次数/秒**|保存点每秒“刷新”的次数（平均值）。 保存点刷新指现有保存点重置为事务生存期中的当前点。|  
|**保存点回滚次数/秒**|事务每秒回滚到保存点的次数（平均值）。|  
|**创建的保存点数/秒**|每秒创建的保存点数（平均值）。|  
|**事务验证失败数/秒**|每秒验证失败的事务数（平均值）。|  
|**用户中止的事务数/秒**|用户每秒中止的事务数（平均值）。|  
|**中止的事务数/秒**|（用户和系统）每秒中止的事务数（平均值）。|  
|**创建的事务数/秒**|系统中每秒创建的事务数（平均值）。<br /><br /> 对 XTP 事务的计数方式不同于基于磁盘的事务（反映在“数据库:事务数/秒”中）。 例如，“创建的事务数/秒”对只读事务进行计数，而“数据库:事务数/秒”则不然。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server XTP（内存中 OLTP）性能计数器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
