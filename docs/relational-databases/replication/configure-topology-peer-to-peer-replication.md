---
title: 配置拓扑（对等复制）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.peers.f1
ms.assetid: 5377c59f-2e25-4852-a306-c87ae3dca9fd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edd8ea9a11a06182dced486ed1b03f1b916e15e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793251"
---
# <a name="configure-topology-peer-to-peer-replication"></a>配置拓扑（对等复制）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以使用 **“配置拓扑”** 页执行常见的配置任务，如添加新节点、删除节点，以及在现有节点之间添加新连接。 在此向导的 **“发布”** 页上选定的节点会显示在设计图面上。 若要指定配置选项，请右键单击某个节点、连接或者设计图面。  
  
> [!NOTE]  
>  配置对等拓扑向导关闭时请求拓扑信息。 如果该向导在所有节点响应信息请求之前关闭并重新打开，则该向导可能会显示部分网络。  
  
## <a name="options"></a>选项  
 **“配置拓扑”** 页包含界面元素和在右键单击元素后显示的选项。 下表对每一界面元素进行了介绍。  
  
|界面元素|描述|  
|-----------------------|-----------------|  
|设计图面|显示其他界面元素。 若要添加元素，请右键单击设计图面。|  
|![拓扑中的第一个节点](../../relational-databases/replication/media/p2pwizard-firstnode.gif "拓扑中的第一个节点")|拓扑中的原始节点。 可使用来自原始节点的发布数据库副本初始化新节点。|  
|![我们具有其完整信息的节点](../../relational-databases/replication/media/p2pwizard-complete.gif "我们具有其完整信息的节点")|运行 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本的实例的节点，复制具有其完整信息。 若要指定配置选项，请右键单击此节点。|  
|![我们具有其不完整信息的节点](../../relational-databases/replication/media/p2pwizard-incomplete.gif "我们具有其不完整信息的节点")|复制具有其不完整信息的节点。 若要指定配置选项，请右键单击此节点。<br /><br /> 复制具有的信息不完整，原因为以下之一：<br /><br /> - 节点运行的是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]实例，该实例没有存储向导所需的所有元数据。<br /><br /> - 节点运行的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的更高版本，但是复制无法从此节点检索订阅信息。 针对此情况进行故障排除：<br /><br /> 确保此节点上的数据库为联机状态，并可使用连接到此节点的分发代理使用的同一凭据连接到此数据库。<br /><br /> 确保连接到此节点的日志读取器代理和所有分发代理当前都在运行。<br /><br /> 确保设置的刷新超时足够长以收集所有拓扑信息。 若要设置超时，请右键单击设计图面，然后单击 **“设置刷新超时”**。|  
|灰色箭头线|两个节点之间的连接。 若要添加连接，请右键单击要连接的节点之一。 若要删除某连接，请右键单击该连接。<br /><br /> 如果箭头线上只有一个箭头，则表明复制拥有的其中一个节点的信息不完整。|  
  
### <a name="options-for-the-design-surface"></a>设计图面选项  
 **重绘图形**  
 重绘设计图面上的对象而不刷新拓扑。 重绘操作可以提供一个更好的拓扑视图。  
  
 **刷新拓扑**  
 查询拓扑中每一节点，然后显示更新后的节点信息。 如果节点数目较大，此过程可能需要几分钟。  
  
 如果向导请求拓扑信息，而您未等到所有节点都响应此请求就关闭并重新打开了向导，则页面可能不会显示拓扑中的所有节点。  
  
 **添加新的对等节点**  
 向对等拓扑添加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 如果将某实例添加为节点，在向导完成后会在该实例上创建一个发布。 添加该节点后，右键单击该节点可在此新节点和现有节点之间添加连接。  
  
 若要加入对等拓扑，实例必须满足以下要求：  
  
-   实例必须已经配置为分发服务器，或者已与远程分发服务器关联。  
  
-   实例必须包含复制所涉及数据库的副本。 此副本通常是原始发布数据库的已还原备份。  
  
 **选择要查看的节点**  
 选择要在设计图面上查看的节点。 如果拓扑包含大量节点，则此选项颇为有用。 请注意，您只能在设计图面上可见的节点间添加连接。  
  
 **“设置刷新超时”**  
 指定刷新过程在超时之前可以运行的时间。  
  
### <a name="options-for-each-node"></a>每个节点的选项  
 **添加新的对等连接**  
 在两个节点之间添加连接。 例如，如果要在节点 A 和节点 B 之间添加连接，则复制会添加两个订阅：第一个订阅使节点 A 可以接收来自节点 B 上的发布的更改，第二个订阅使节点 B 可以接收来自节点 A 上的发布的更改。  
  
 **删除对等节点**  
 从拓扑中删除节点。 例如，如果删除了节点 C，则该节点上的发布也会删除。 节点 A 和节点 C 以及节点 B 和节点 C 之间的订阅也会删除。 而节点 C 上的数据库不会删除，发布和分发也不会禁用。  
  
> [!NOTE]  
>  配置对等复制时，可以为每个节点指定一个 ID。 此 ID 对于拓扑中的所有节点必须是唯一的，存储于 [MSpeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系统表的 originator_id 列中。 如果从拓扑中删除节点，此 ID 仍会保留在历史记录表中。 保留此 ID 是为了防止当存在来自整个拓扑中仍在复制的已删除节点的更改时出现虚假冲突。 如果想要对新节点重新使用该 ID，必须首先从所有节点 MSpeer_originatorid_history 表中手动删除该 ID。 在删除节点的 ID 之前，请执行 [sp_requestpeerresponse](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 以确保复制从该节点进行的所有更改。  
  
 **连接到所有显示的节点**  
 在选定节点和所有其他节点之间添加连接。 例如，如果您在有三个节点的拓扑中为节点 C 选定了此选项，则复制会添加四个订阅：其中两个订阅使节点 A 和节点 B 可以接收来自节点 C 上的发布的更改，而另两个订阅使节点 C 可以接收来自节点 A 和节点 B 上的发布的更改。  
  
 **选择要查看的节点**  
 选择要在设计图面上查看的节点。 如果拓扑包含大量节点，则此选项颇为有用。 请注意，您只能在设计图面上可见的节点间添加连接。  
  
### <a name="options-for-the-connection-arrows"></a>针对连接箭头的选项  
 **删除对等连接**  
 删除两个节点之间的连接。 例如，如果要删除节点 A 和节点 B 之间的连接，则复制会删除两个订阅：一个订阅使节点 A 可以接收来自节点 B 上的发布的更改，另一个订阅使节点 B 可以接收来自节点 A 上的发布的更改。  
  
## <a name="see-also"></a>另请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [管理对等拓扑（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
