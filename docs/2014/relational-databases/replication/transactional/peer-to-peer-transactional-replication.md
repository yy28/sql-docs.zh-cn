---
title: 对等事务复制 | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
- transactional replication, peer-to-peer replication
- peer-to-peer transactional replication
ms.assetid: 23e7e8c1-002f-4e69-8c99-d63e4100de64
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 133d44d233abdcffe7893ce29be5b462f4b16524
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127187"
---
# <a name="peer-to-peer-transactional-replication"></a>@loopback_detection
  对等复制通过在多个服务器实例（又称为“节点” ）上维护数据副本，提供了一种扩展的高可用性解决方案。 对等复制建立在事务复制的基础之上，以事务方式近乎实时地传播一致的更改。 这样，需要扩展读取操作的应用程序就可以将来自客户端的读取操作分布到多个节点上。 由于对等复制以近乎实时的方式维护节点上的数据，从而提供了数据冗余，提高了数据的可用性。  
  
 请考虑 Web 应用程序的情况。 它可以通过以下方式从对等复制中获益：  
  
-   目录查询和其他读取操作被分散到多个节点上。 这样，当读取操作增多时，仍能够保持原有的性能。  
  
-   如果系统中的某个节点失效，应用层可将该节点的写入操作重定向到其他节点。 这样便可保持可用性。  
  
-   如果节点需要维护或整个系统需要升级，则可以将各个节点脱机并在完成操作后再将其重新添加回系统中，而不影响到应用程序的可用性。  
  
 虽然对等复制可扩展读取操作，但对于单个节点而言，该拓扑的写入性能也同样出色。 这是因为所有的插入、更新和删除操作最终都会传播到所有节点上。 复制可识别出更改已应用于给定节点这一情况，避免在节点间多次循环应用更改。 强烈建议仅在节点上执行每一行的写入操作，理由如下：  
  
-   如果在多个节点上修改了某一行，则将该行传播给其他节点时会导致冲突甚至丢失更新。  
  
-   复制更改时总是存在一定的延迟。 对于要求立即显示最新更改的应用程序而言，在多个节点上对应用程序执行动态负载平衡可能会出现问题。  
  
 对等复制包括了在对等拓扑中启用冲突检测的选项。 此选项有助于防止因未检测到的冲突引起的各种问题，包括不一致的应用程序行为和丢失更新。 启用该选项后，默认情况下，发生冲突的更改被视为导致分发代理失败的关键错误。 发生冲突时，拓扑将始终处于不一致的状态，直至手动解决冲突并使拓扑中的数据一致。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
> [!NOTE]  
>  为了避免潜在的数据不一致性，即便已经启用了冲突检测功能，也应尽力避免对等拓扑中发生冲突。 为了确保仅在某一个节点上执行特定行的写入操作，访问并更改数据的应用程序必须对其插入、更新和删除操作进行分区。 分区可确保在一个节点上对给定行的修改可以在其他节点修改该行之前，与拓扑中所有其他节点同步。 如果应用程序需要完善的冲突检测与解决功能，请使用合并复制。 有关详细信息，请参阅[合并复制](../merge/merge-replication.md)和[检测并解决合并复制冲突](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
## <a name="peer-to-peer-topologies"></a>对等拓扑  
 下列方案说明了对等复制的典型应用。  
  
### <a name="topology-that-has-two-participating-databases"></a>包含两个参与数据库的拓扑  
 ![对等复制，两节点](../media/repl-multinode-01.gif "对等复制，两节点")  
  
 上面两张图均显示了两个参与数据库，其中通过应用程序服务器将用户流量定向到数据库。 此配置可用于从网站到工作组应用程序等多种应用程序，并具有下列优点：  
  
-   由于将读取操作分散到两台服务器上，因此提高了读取的性能。  
  
-   当需要维护或某一节点出现故障时，可以提供更高的可用性。  
  
 从这两张图中可以看到，读取活动在参与数据库间进行负载平衡，但更新的处理方式则有所不同：  
  
-   在左图中，在两台服务器间对更新进行了分区。 例如，如果数据库包含产品目录，则可以令自定义应用程序把对名称以 A-M 开头的产品进行的更新定向到节点 **A** ，把对名称以 N-Z 开头的产品进行的更新定向到节点 **B** 。然后将更新复制到另一个节点。  
  
-   在右侧，所有更新都定向到节点 **B**。从那里，更新被复制到节点 **A**。如果节点 **B** 脱机（例如，进行维护），则应用程序服务器可以将所有活动定向到节点 **A**。当节点 **B** 恢复联机状态后，更新便可流向 B，并且应用程序服务器可以将所有更新移动回节点 **B**，也可以继续将更新定向到节点 **A**。  
  
 对等复制对这两种方法均支持，但右图中的中心更新示例也经常同标准事务复制一起使用。  
  
### <a name="topologies-that-have-three-or-more-participating-databases"></a>包含三个或三个以上参与数据库的拓扑  
 ![向分散位置的对等复制](../media/repl-multinode-02.gif "向分散位置的对等复制")  
  
 上图显示了三个参与数据库，它们为一家在洛杉矶、伦敦和台北均设有办事处的国际软件支持机构提供数据。 每个办事处的支持工程师接听客户电话，并输入和更新每个客户电话的相关信息。 三个办事处的时区各相差八小时，因此不会出现工作日的重叠。 台北办事处下班时，伦敦办事处正开始一天的工作。 如果办事处下班时电话仍在进行中，则电话将被转接到下一个开始办公的办事处的代表。  
  
 每个地点都有一台数据库服务器和一台应用程序服务器，供支持工程师在输入和更新客户电话的相关信息时使用。 拓扑按时间进行分区。 因此更新只发生在正在办公的节点，然后更新会流动到其他参与数据库。 此拓扑具有下列优点：  
  
-   独立但不孤立：每个办公室可以插入、 更新或单独删除数据但还可以共享数据，因为它复制到所有其他参与数据库。  
  
-   在出现故障或需要维护一个或多个参与数据库时可提供更高的可用性。  
  
     ![对等复制，三节点和四节点](../media/repl-multinode-04.gif "对等复制，三节点和四节点")  
  
 上图显示了向三节点拓扑添加节点的过程。 在此应用情景中，可能会由于以下原因再添加一个节点：  
  
-   因为又开设了一家办事处。  
  
-   为了提供更高的可用性以支持维护或提高发生磁盘故障或其他重大故障时的容错能力。  
  
 请注意，在三节点拓扑和四节点拓扑中，所有的数据库都向其他数据库发布和订阅数据。 在需要进行维护或者一个或多个节点发生故障时，这样可提供最大的可用性。 添加节点后，必须针对性能以及部署和管理的复杂性来权衡可用性和可伸缩性的需要。  
  
## <a name="configuring-peer-to-peer-replication"></a>配置对等复制  
 配置对等复制拓扑的过程与配置一系列标准事务发布和订阅的过程非常类似。 下列主题中介绍的步骤演示一个三节点系统的配置过程，该系统类似于上面显示对等拓扑的左图中的配置。  
  
## <a name="considerations-for-using-peer-to-peer-replication"></a>使用对等复制的注意事项  
 本节提供在使用对等复制时要考虑的信息和指导原则。  
  
### <a name="general-considerations"></a>一般注意事项  
  
-   对等复制仅在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的 Enterprise 版本中提供。  
  
-   所有参与对等复制的数据库都应包含相同的架构和数据：  
  
    -   对象名称、对象架构和发布名称都应相同。  
  
    -   发布必须允许复制架构更改。 （这相当于发布属性**replicate_ddl** 设置为 **1**，这是默认设置）。有关详细信息，请参阅[对发布数据库进行架构更改](../publish/make-schema-changes-on-publication-databases.md)。  
  
    -   不支持行筛选和列筛选。  
  
-   建议每个节点都使用自己的分发数据库。 这样将消除出现单点故障的可能性。  
  
-   表和其他对象不能包含在一个发布数据库内的多个对等发布中。  
  
-   必须为对等复制启用发布后，才能创建订阅。  
  
-   必须使用备份或 **replication support only** 选项对订阅进行初始化。 有关详细信息，请参阅[在没有快照的情况下初始化事务订阅](../initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
-   建议不要使用标识列。 使用标识时，必须手动管理所分配的每个参与数据库中表的范围。 有关详细信息，请参阅[复制标识列](../publish/replicate-identity-columns.md)中的“为手动标识范围管理分配范围”部分。  
  
### <a name="feature-restrictions"></a>功能限制  
 对等复制支持事务复制的核心功能，但不支持以下选项：  
  
-   使用快照进行初始化和重新初始化。  
  
-   行筛选器和列筛选器。  
  
-   时间戳列。  
  
-   非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的发布服务器和订阅服务器。  
  
-   立即更新订阅和排队更新订阅。  
  
-   匿名订阅。  
  
-   部分订阅。  
  
-   可附加的订阅和可转换的订阅。 （在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]中不推荐使用这两个选项。）  
  
-   共享分发代理。  
  
-   分发代理参数 **-SubscriptionStreams** 和日志读取器代理参数 **-MaxCmdsInTran**。  
  
-   项目属性 **@destination_owner** 和 **@destination_table**）上维护数据副本，提供了一种扩展的高可用性解决方案。  

-   对等事务复制不支持创建针对对等发布的单向事务订阅
  
 以下属性具有特殊的注意事项：  
  
-   发布属性**@allow_initialize_from_backup**的值需要为`true`。  
  
-   项目属性**@replicate_ddl**的值需要为`true`;**@identityrangemanagementoption**的值需要为`manual`; 并**@status**需要该选项**24**设置。  
  
-   项目属性的值**@ins_cmd**， **@del_cmd**，以及**@upd_cmd**不能设置为`SQL`。  
  
-   订阅属性**@sync_type**的值需要为`none`或`automatic`。  
  
### <a name="maintenance-considerations"></a>维护注意事项  
 下列操作需要让系统静止。 也就是说，停止所有节点上已发布表中的活动，并确保每个节点都已收到来自所有其他节点的更改。  
  
-   添加[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]向现有拓扑的节点  
  
-   将项目添加到现有发布  
  
-   进行架构更改  
  
-   从备份还原节点  
  
 有关详细信息，请参阅[停止复制拓扑（复制 Transact-SQL 编程）](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)和[管理对等拓扑（复制 Transact-SQL 编程）](../administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)。  
  
-   如果要将新节点添加到对等拓扑中，只应从在添加新节点后创建的备份中进行还原。  
  
-   无法重新初始化对等拓扑中的订阅。 如果需要确保节点有新的数据副本，请在该节点上还原备份。  
  
## <a name="see-also"></a>请参阅  
 [管理对等拓扑（复制 Transact-SQL 编程）](../administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [快照复制和事务复制的备份和还原策略](../administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)   
 [事务复制的发布类型](transactional-replication.md)  
  
  
