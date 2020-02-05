---
title: 高级冲突检测和解决（合并）
description: 了解通过合并复制检测和解决冲突的高级方法。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f90625c1aa123cf72b93ce815b02cccd7cedc78a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321590"
---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>高级合并复制 - 冲突的检测和解决
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  当发布服务器与订阅服务器连接并进行同步时，合并代理将检测是否存在任何冲突。 如果检测到冲突，合并代理将使用冲突解决程序（将项目添加到发布时指定的）来确定接受哪些数据并将其传播到其他站点。  

 合并复制提供了多种检测和解决冲突的方法。 此默认方法适用于大多数应用程序：  
  
-   如果发布服务器和订阅服务器发生冲突，则保留发布服务器更改，而放弃订阅服务器更改。   
-   如果使用客户端订阅（请求订阅的默认类型）的两台订阅服务器发生冲突，则保留第一台与发布服务器同步的订阅服务器的更改，而放弃第二台订阅服务器的更改。 有关指定客户端和服务器订阅的信息，请参阅[指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。   
-   如果使用服务器订阅（推送订阅的默认类型）的两台订阅服务器发生冲突，则保留具有最高优先级值的订阅服务器的更改，而放弃另一台订阅服务器的更改。 如果优先级值相等，则保留第一台与发布服务器同步的订阅服务器的更改。  
  
> [!NOTE]  
>  由于订阅服务器与发布服务器同步，因此冲突通常发生在不同订阅服务器上进行的更新之间，而不是发生在订阅服务器和发布服务器上进行的更新之间。  
  
 冲突的检测和解决行为取决于下列选项，本主题对这些选项进行了说明：    
-   指定列级跟踪、行级跟踪还是逻辑记录级跟踪。    
-   指定默认的基于优先级的解决机制，还是指定项目冲突解决程序。 项目冲突解决程序可以是：  
  
    -   以托管代码编写的  业务逻辑处理程序。   
    -   基于 COM 的自定义冲突解决程序  。    
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]提供的基于 COM 的冲突解决程序。  
  
     如果使用的是默认解决机制，则冲突的检测和解决行为还取决于所用的订阅类型：客户端或服务器。  
  
## <a name="conflict-detection"></a>冲突检测  
 数据更改是否可视为冲突取决于为项目设置的冲突跟踪类型：  
  
-   选择列级冲突跟踪时，如果对多个复制节点的同一行中的同一列进行更改，则此更改视为冲突。    
-   选择行级跟踪时，如果对多个复制节点的同一行中的任意列进行更改（相应行中受影响的列不必相同），则此更改视为冲突。    
-   选择逻辑记录级跟踪时，如果对多个复制节点的同一逻辑记录中的任意行进行更改（相应行中受影响的列不必相同），则此更改视为冲突。  
  
 有关详细信息，请参阅 [检测并解决逻辑记录中的冲突](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)。  
  
 若要指定项目的冲突跟踪和解决方法级别，请参阅[修改合并复制属性](../../../relational-databases/replication/merge/specify-merge-replication-properties.md)。  
  
## <a name="conflict-resolution"></a>冲突解决  
 检测到冲突后，合并代理将启动选定的冲突解决程序，并使用该冲突解决程序来确定冲突解决入选方。 入选行将应用到发布服务器和订阅服务器，而落选行中的数据将写入冲突表。 除非选择交互解决冲突，否则冲突解决程序一经执行就会立即解决冲突。  

解决合并复制冲突  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  当发布服务器与订阅服务器连接并进行同步时，合并代理将检测是否存在任何冲突。 如果检测到冲突，合并代理将使用冲突解决程序来确定将接受哪些数据并将其传播到其他站点。  
  
> [!NOTE]  
>  虽然订阅服务器与发布服务器同步，但冲突通常发生于不同订阅服务器上进行的更新之间，而不是于订阅服务器和发布服务器上进行的更新之间。  
  
 合并复制提供了多种检测和解决冲突的方法。 此默认方法适用于大多数应用程序：  
  
-   如果发布服务器和订阅服务器发生冲突，则保留发布服务器更改，而放弃订阅服务器更改。  
  
-   如果使用客户端订阅（请求订阅的默认类型）的两台订阅服务器发生冲突，则保留第一台与发布服务器同步的订阅服务器的更改，而放弃第二台订阅服务器的更改。 有关指定客户端和服务器订阅的信息，请参阅[指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。  
  
-   如果使用服务器订阅（推送订阅的默认类型）的两台订阅服务器发生冲突，则保留具有最高优先级值的订阅服务器的更改，而放弃另一台订阅服务器的更改。 如果优先级值相等，则保留第一台与发布服务器同步的订阅服务器的更改。  
  
 有关合并复制的冲突检测和解决的详细信息，请参阅 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
### <a name="resolver-types"></a>冲突解决程序类型  
 在合并复制中，冲突解决发生在项目级别。 对于由多个项目组成的发布，可以用不同的冲突解决程序解决不同项目的冲突，也可以用同一个冲突解决程序解决一个项目、多个项目或者组成发布的所有项目的冲突。  
  
 如果计划使用默认的基于优先级的冲突解决程序，则不必设置项目的冲突解决程序属性。 如果想使用项目冲突解决程序（而不是默认冲突解决程序），则必须为要使用该程序的项目设置冲突解决程序属性，可以通过在发布服务器上选择一个可用的冲突解决程序来进行设置。 任何需要传递到冲突解决程序的特定信息也可以在冲突解决程序信息属性中指定。  
  
 合并复制提供了四种的冲突解决程序：  
  
-   默认的基于优先级的冲突解决程序  
  
     默认解决机制的行为不同，具体取决于订阅是客户端订阅还是服务器订阅。 为使用服务器订阅的各个订阅服务器指定优先级值；当出现任何冲突时，在具有最高优先级的节点上发生的更改将会入选。 对于客户端订阅，发生冲突时，第一个写入发布服务器的更改将会入选。  
  
     创建订阅后，将无法更改其类型。  
  
-   业务逻辑处理程序  
  
     通过使用业务逻辑处理程序框架，您可以编写合并同步过程中调用的托管代码程序集。 程序集包括可以响应同步期间的冲突和多种其他情况的业务逻辑。 有关详细信息，请参阅[合并同步期间执行业务逻辑](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
-   基于 COM 的自定义冲突解决程序  
  
     合并复制提供了 API，通过该 API 可以用各种语言（如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]）将冲突解决程序编写为 COM 对象。 有关详细信息，请参阅 [COM-Based Custom Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)。  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包括许多基于 COM 的解决程序。 有关详细信息，请参阅 [Microsoft 基于 COM 的冲突解决程序](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
 有关如何选择适当类型的冲突解决程序的信息，请参阅[选择冲突解决程序](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md)。  
  
> [!NOTE]  
>  某些项目冲突解决程序经编写可仅处理特定操作的冲突。 例如，某个冲突解决程序可能处理更新操作的冲突，但不处理插入或删除操作的冲突。 默认的基于优先级的冲突解决程序处理项目冲突解决程序未处理的任何冲突。  
  
 若要指定合并订阅类型和冲突解决优先级，请参阅  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   复制 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 编程和复制管理对象 (RMO) 编程： [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md) 和 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>交互式冲突解决程序  
 复制提供了一个交互式冲突解决程序用户界面，它可以与默认的基于优先级的冲突解决程序或项目冲突解决程序一起使用。 通过 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 同步管理器执行按需同步时，交互式冲突解决程序在运行时显示冲突数据，并让用户选择解决冲突的方式。 有关如何启用交互式解决方法并启动交互式冲突解决程序的详细信息，请参阅 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
## <a name="viewing-conflicts"></a>查看冲突  
 查看冲突最简单的方法是使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 提供的复制冲突查看器（[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还提供了可以查询冲突表的存储过程）。 冲突查看器和交互式冲突解决程序是类似的工具，但交互式冲突解决程序使用户可以在同步发生时解决冲突，而冲突查看器则用于查看已解决的冲突。 如果冲突元数据仍存在于系统表中（默认情况下，冲突元数据保留 14 天），则可以覆盖冲突查看器中的冲突解决结果，但如果需要定期对其进行直接干预，则请考虑使用交互式冲突解决程序。  
  
> [!NOTE]  
>  包含逻辑记录的冲突不会显示在冲突查看器中。 若要查看有关这些冲突的信息，请使用复制存储过程。 有关详细信息，请参阅[查看合并发布的冲突信息（复制 Transact-SQL 编程）](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)。  
  
 冲突查看器显示来自三个系统表的信息：  
  
-   复制会为合并项目中的每个表创建一个冲突表，该冲突表的名称格式为 **MSmerge_conflict_\<PublicationName>_\<ArticleName>** 。  
  
     冲突表与其所依据的表具有相同的结构。 其中某个冲突表中的一行由冲突行的落选版本（冲突行的入选版本位于实际用户表中）组成。  
  
-   **MSmerge_conflicts_info** 表提供了每个冲突的相关信息，包括冲突类型。  
  
-   表 **sysmergearticles** 标识了具有冲突表的用户表，并提供了冲突表的相关信息。  
  
 默认情况下，冲突信息存储在下列位置：  
  
-   如果发布兼容级别为 90RTM 或更高，则存储在发布服务器和订阅服务器上。  
  
-   如果发布兼容级别低于 80RTM，则存储在发布服务器上。  
  
-   如果订阅服务器运行的是 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]，则存储在发布服务器上。 冲突数据不能存储在 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 订阅服务器上。  
  
 **查看冲突**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[查看和解决合并发布的数据冲突 (SQL Server Management Studio)](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   复制 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 编程：[查看合并发布的冲突信息（复制 Transact-SQL 编程）](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>另请参阅  
 [同步数据](../../../relational-databases/replication/synchronize-data.md)  
  
  
