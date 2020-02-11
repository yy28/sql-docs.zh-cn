---
title: 删除数据库镜像 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- stopping database mirroring [SQL Server]
- removing database mirroring [SQL Server]
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 414cdedb8f2bc3dee4edc792c11b6438306818c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62754547"
---
# <a name="removing-database-mirroring-sql-server"></a>删除数据库镜像 (SQL Server)
  数据库所有者可以在任一伙伴上随时手动停止数据库镜像会话。  
  
## <a name="impact-of-removing-mirroring"></a>删除镜像的影响  
 删除镜像时，将发生以下情况：  
  
-   伙伴间的关系以及每个伙伴与见证服务器间的关系都将永久中断（如果存在任何关系）。  
  
     如果在停止会话时伙伴之间正在相互通信，则在两台计算机上的关系将立即中断。 如果伙伴之间未通信（在停止时数据库处于 DISCONNECTED 状态），停止镜像的伙伴上的关系将立即中断；当另一个伙伴试图重新连接时，将会发现数据库镜像会话已经终止。  
  
-   有关镜像会话的信息已经清除，这一点与暂停会话不同。 删除了主体数据库和镜像数据库上的镜像。 在 **sys.databases** 中，**mirroring_state** 列及所有其他镜像列都设置为 NULL。 有关详细信息，请参阅 [sys.database_mirroring (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql)。  
  
-   每台伙伴服务器实例使用的数据库为数据库的单独副本。  
  
-   由于镜像数据库是使用 RESTORE WITH NORECOVERY 创建的，因此镜像数据库的状态为 RESTORING（请查看 **sys.databases** 的 **state**列）。 此时，您可以删除以前的镜像数据库或使用 WITH RECOVERY 还原以前的镜像数据库。 恢复该数据库时，由于恢复将启动新的恢复分支，因此将与以前的主体数据库不同。  
  
> [!NOTE]  
>  若要在停止会话后继续镜像，必须建立新的数据库镜像会话。 如果在停止镜像后创建日志备份，必须在重新启动镜像之前将该日志备份应用到镜像数据库中。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **删除数据库镜像**  
  
-   [删除数据库镜像 (SQL Server)](database-mirroring-sql-server.md)  
  
 **启动数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (Transact-SQL)](database-mirroring-establish-session-windows-authentication.md)  
  

  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)   
 [暂停和恢复数据库镜像 (SQL Server)](pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
