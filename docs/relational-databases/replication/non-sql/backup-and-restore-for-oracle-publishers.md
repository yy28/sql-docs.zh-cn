---
title: "Oracle 发布服务器的备份和还原 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- recovery [SQL Server replication], Oracle publishing
- backups [SQL Server replication], Oracle publishing
- Oracle publishing [SQL Server replication], backup and restore
- restoring [SQL Server replication], Oracle publishing
ms.assetid: e5f181d0-cacf-442b-8b7a-202b3cfc358b
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 802d157cd886f5656513904c0b519a65b61d67b3
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="backup-and-restore-for-oracle-publishers"></a>Oracle 发布服务器的备份和还原
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  在备份和还原时，请遵循以下准则：  
  
-   在备份发布服务器时，确保日志读取器代理未运行，并且未在发布的表上进行其他数据库活动。  
  
-   同时备份发布服务器和分发服务器。  
  
-   如果必须还原发布服务器或分发服务器，请重新初始化所有订阅。  
  
-   若要从备份中还原订阅服务器（无须重新初始化订阅），则订阅数据库最后一次备份完成之后传递到分发数据库的事务必须仍然可用。 事务可用的时间长度取决于分发保持设置。 有关这些设置的信息，请参阅[订阅过期和停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
-   如果由于数据还原造成发布服务器或分发服务器不同步，则复制代理将错误消息写入日志。 此时，必须删除并重新创建所有相关的发布和订阅：  
  
    1.  编写发布和订阅的定义脚本。 有关详细信息，请参阅 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
         如果在发布服务器和分发服务器状态的版本中发布定义有所更改，就需要修改脚本。  
  
    2.  删除发布和订阅。  
  
    3.  运行步骤 1 中创建的脚本。  
  
     如果必须删除和重新配置发布服务器，请使用 **CASCADE** 选项删除 **MSSQLSERVERDISTRIBUTOR** 公共同义词和已配置的 Oracle 复制用户，以便从 Oracle 发布服务器中删除所有复制对象。  
  
## <a name="see-also"></a>另请参阅  
 [备份和还原复制的数据库](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [配置 Oracle 发布服务器](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
