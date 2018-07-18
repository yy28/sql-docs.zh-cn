---
title: 排除失败的添加文件操作 （AlwaysOn 可用性组） 的问题 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09b6d19aad9b0095029405a5e0e4ddb1f7597b61
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289543"
---
# <a name="troubleshoot-a-failed-add-file-operation-alwayson-availability-groups"></a>解决失败的添加文件操作问题（AlwaysOn 可用性组）
  在某些 AlwaysOn 可用性组部署中，文件路径在承载主副本的系统与承载辅助副本的系统之间存在差异。 如果辅助副本上不存在添加文件操作的文件路径，则添加文件操作会在主数据库上取得成功。 但添加文件操作将会导致辅助数据库挂起。 而这又会导致辅助副本进入“非同步”状态。  
  
> [!NOTE]  
>  我们建议，如有可能，给定辅助数据库的文件路径（包括驱动器号）应该与相应的主数据库的路径相同。  
  
## <a name="problem-resolution"></a>问题解决方案  
 若要解决此问题，数据库所有者必须完成以下步骤：  
  
1.  从可用性组中删除辅助数据库。 有关详细信息，请参阅[从可用性组中删除辅助数据库 (SQL Server)](remove-a-secondary-database-from-an-availability-group-sql-server.md)。  
  
2.  在现有辅助数据库上，使用 WITH NORECOVERY 和 WITH MOVE（指定将承载辅助副本的服务器实例上的文件路径）将包含添加的文件的文件组的完整副本还原到辅助数据库。 有关详细信息，请参阅[将数据库还原到新位置 (SQL Server)](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)。  
  
3.  备份包含对主数据库的添加文件操作的事务日志，并且使用 WITH NORECOVERY 和 WITH MOVE 手动还原辅助数据库上的日志备份。  
  
4.  通过使用 WITH NO RECOVERY 从主数据库还原任何其他待定日志备份，对辅助数据库进行准备以便重新联接到可用性组。  
  
5.  将辅助数据库重新联接到可用性组。 有关详细信息，请参阅 [将辅助数据库联接到可用性组 (SQL Server)](join-a-secondary-database-to-an-availability-group-sql-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [为可用性组手动准备辅助数据库 (SQL Server)](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [孤立用户故障排除 (SQL Server)](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [解决 AlwaysOn 可用性组配置问题&#40;SQL Server&#41;删除](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
