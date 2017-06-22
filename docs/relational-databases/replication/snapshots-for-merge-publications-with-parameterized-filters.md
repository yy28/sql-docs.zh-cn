---
title: "带有参数化筛选器的合并发布的快照 | Microsoft Docs"
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
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 246e2e5db5c3e64973c165be8b03e03b7c8226a5
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>带有参数化筛选器的合并发布的快照
  在合并发布中使用参数化行筛选器时，复制将使用由两部分构成的快照初始化各个订阅。 首先，创建一个架构快照，该快照包含复制所需的所有对象和已发布对象的架构，但不包含数据。 然后，使用快照初始化每个订阅，该快照包含架构快照中的对象和架构以及属于订阅分区的数据。 如果多个订阅接收某个给定分区（即这些订阅接收相同的架构和数据），则该分区的快照只创建一次；多个订阅通过使用相同的快照来初始化。 有关参数化行筛选器的详细信息，请参阅 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
 可以采用下列三种方法之一为包含参数化筛选器的发布创建快照：  
  
-   为每个分区预生成快照。 使用此选项可控制快照生成时间。  
  
     您也可以选择按计划刷新快照。 订阅创建了快照的分区的新订阅服务器将接收最新的快照。  
  
-   允许订阅服务器在第一次同步时请求快照生成和应用。 使用此选项允许新订阅服务器无需请求管理员干预即可进行同步（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理必须在发布服务器上运行以便能够生成快照）。  
  
    > [!NOTE]  
    >  如果发布中对一个或多个项目的筛选生成了对每个订阅具有唯一性的非重叠分区，则每当运行合并代理时都会清除元数据。 这意味着分区快照会过期得更快。 使用此选项时，应考虑允许订阅服务器启动快照的生成和传递。 有关筛选选项的详细信息，请参阅 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
-   使用快照代理为每台订阅服务器手动生成一个快照。 然后，订阅服务器必须为合并代理提供快照位置，使之可检索和应用正确的快照。  
  
    > [!NOTE]  
    >  支持此选项是为了向后兼容，此选项不允许 FTP 快照共享。  
  
 最灵活的方法是组合使用预生成的快照选项和订阅服务器请求的快照选项：按计划（通常在非高峰时段）预生成快照和刷新快照，但如果创建了需要新分区的订阅，则订阅服务器可以生成自己的快照。  
  
 例如 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]，它完成将库存情况传递到各个店铺的行动任务。 每个销售人员都接收到依据各自登录帐户的订阅（检索销售人员所工作店铺的数据）。 管理员选择预生成快照并在每个星期日刷新快照。 偶而会有新用户添加到系统中，并需要尚无快照的分区的数据。 管理员也选择允许订阅服务器启动的快照，以避免出现因为尚无快照而使订阅服务器无法订阅发布的情况。 当新订阅服务器第一次连接时，将为指定分区生成快照，并将快照应用于订阅服务器上（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理必须在发布服务器上运行以便能够生成快照）。  
  
 若要为包含参数化筛选器的发布创建快照，请参阅 [为包含参数化筛选器的合并发布创建快照](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
## <a name="security-settings-for-the-snapshot-agent"></a>快照代理的安全设置  
 快照代理为每个分区创建快照。 对于预生成的快照和订阅服务器请求的快照，代理使用在创建发布的快照代理作业时（该作业通过新建发布向导或 **sp_addpublication_snapshot**创建）指定的凭据运行和进行连接。 若要更改凭据，请使用 **sp_changedynamicsnapshot_job**。 有关详细信息，请参阅 [sp_changedynamicsnapshot_job (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [保护快照文件夹](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
