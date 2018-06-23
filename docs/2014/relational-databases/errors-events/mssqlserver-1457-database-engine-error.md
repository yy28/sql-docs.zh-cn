---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f103b4b2eb1538b9c4eff8e804781f1866c38b95
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013858"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1457|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_PAGE_UNDO_PENDING|  
|消息正文|镜像数据库 '%.*ls' 的同步操作中断，导致数据库处于不一致的状态。 ALTER DATABASE 命令失败。 请确保镜像数据库重新启动并联机，然后重新连接镜像服务器实例，并允许镜像数据库完成同步。|  
  
## <a name="explanation"></a>解释  
 此消息表明 ALTER DATABASE *database_name* SET PARTNER OFF 语句失败。 尝试删除数据库镜像操作失败导致镜像数据库的同步操作中断。 数据库处于不一致状态。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，您可以执行下列某种操作：  
  
-   恢复镜像服务器和主体服务器之间的连接以允许镜像数据库同步。  
  
-   删除镜像数据库。  
  
     删除镜像数据库后，可以从备份创建一个新的镜像数据库。  
  
    > [!NOTE]  
    >  如果仍只是在 SET PARTNER OFF 语句失败后启用镜像，则可以删除镜像数据库。  
  
## <a name="see-also"></a>请参阅  
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [设置数据库镜像 (SQL Server)](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [删除数据库镜像 (SQL Server)](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [为镜像准备镜像数据库 (SQL Server)](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
  
