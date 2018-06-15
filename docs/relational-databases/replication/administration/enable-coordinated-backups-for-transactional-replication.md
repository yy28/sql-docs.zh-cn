---
title: 为事务复制启用协调备份 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, backup and restore
- sp_replicationdboption
- sync with backup [SQL Server replication]
- coordinated backups [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62799acad263397d61db1c474de776019d1b5b8d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32955502"
---
# <a name="enable-coordinated-backups-for-transactional-replication"></a>为事务复制启用协调备份
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在为数据库启用事务复制时，可以指定在传递到分发数据库之前必须备份所有事务。 也可以对分发数据库启用协调备份，以便在传播到分发服务器的事务未备份前不会截断发布数据库的事务日志。 有关详细信息，请参阅 [快照复制和事务复制的备份和还原策略](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
### <a name="to-enable-coordinated-backups-for-a-database-published-with-transactional-replication"></a>为与事务复制一起发布的数据库启用协调备份  
  
1.  在发布数据库中，使用 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 函数返回发布数据库的 **IsSyncWithBackup** 属性。 如果函数返回 **1**，则表明已为发布的数据库启用了协调备份。  
  
2.  如果步骤 1 中的函数返回 **0**，则在发布服务器的发布数据库中执行 [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 为 **@optname** 指定值 **@optname**，并为 **@value** 指定值 **@value**。  
  
    > [!NOTE]  
    >  如果将 **sync with backup** 选项更改为 **false**，则运行日志读取器代理或达到运行间隔（如果日志读取器代理配置为连续运行）之后将更新发布数据库的截断点。 最大间隔由 **–MessageInterval** 代理参数控制（默认值为 30 秒）。  
  
### <a name="to-enable-coordinated-backups-for-a-distribution-database"></a>为分发数据库启用协调备份  
  
1.  在发布数据库中，使用 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) 函数返回分发数据库的 **IsSyncWithBackup** 属性。 如果函数返回 **1**，则表明已为分发数据库启用了协调备份。  
  
2.  如果步骤 1 中的函数返回 **0**，则在分发服务器的分发数据库中执行 [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 为 **@optname** 指定值 **@optname** ，并为 **@value** 指定值 **@value**。  
  
### <a name="to-disable-coordinated-backups"></a>禁用协调备份  
  
1.  在发布服务器的发布数据库或在分发服务器的分发数据库中，执行 [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。 为 **@optname** 指定值 **@optname** ，并为 **false** 指定值 **@value**。  
  
  
