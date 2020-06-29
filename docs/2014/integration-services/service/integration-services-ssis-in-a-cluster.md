---
title: 群集中的 Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1cb82571c09aea186ebc76894a4b316e03e4b50e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421864"
---
# <a name="integration-services-ssis-in-a-cluster"></a>群集中的 Integration Services (SSIS)
  建议不要对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 进行聚类分析，因为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不是群集服务或群集感知服务，而且不支持从一个群集节点故障转移到另一个节点。 因此，在群集环境内，应当在群集的每个节点上安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 并将其作为一个独立服务来启动。  
  
 虽然 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不是群集服务，但您可以在将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务单独安装在群集的每个节点上之后，手动将该服务配置为作为群集资源运行。  
  
 但是，如果您建立群集硬件环境的目的是实现高可用性，那么，不将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源也可以实现此目标。  若要从群集中的其他任何节点管理该群集中某一节点上的包，请在群集的每个节点上修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置文件。 可以修改每个配置文件，使其指向包所存储到的所有可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 本解决方案提供大多数客户所需的高可用性，而不会带来在将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源时可能遇到的问题。 有关如何更改此配置文件的详细信息，请参阅[配置 Integration Services 服务（SSIS 服务）](integration-services-service-ssis-service.md)  
  
 了解 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的角色对于就如何在群集环境中配置该服务做出明智决定至关重要。 有关详细信息，请参阅 [Integration Services 服务（SSIS 服务）](integration-services-service-ssis-service.md)。  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>了解将 Integration Services 配置为群集资源的缺点  
 将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为群集资源的一些潜在缺点包括：  
  
-   发生故障转移时，正在运行的包不重新启动。 可以通过从检查点重新启动包来从包失败中恢复。 可以从检查点重新启动，而不必将服务配置为群集资源。 有关详细信息，请参阅 [通过使用检查点重新启动包](../packages/restart-packages-by-using-checkpoints.md)。  
  
-   在不同于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的资源组中配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务时，不能使用客户端计算机上的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 来管理存储在 msdb 数据库中的包。 在这个双跃点方案中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务不能委托凭据。  
  
-   如果群集内有多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源组包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，则故障转移可能会导致意外的结果。 请考虑以下场景。 组 1 运行于节点 A 上，其中包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。组 2 运行于节点 B 上，其中也包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。组 2 故障转移到节点 A。由于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务是单实例服务，因此尝试在节点 A 上启动 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的另一个实例时将失败。 尝试故障转移到节点 A 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务是否也失败取决于组 2 中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的配置。 如果 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为影响资源组中的其他服务，那么，由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务失败，因此正在故障转移的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务也将失败。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务配置为不影响资源组中的其他服务，则该服务将能够故障转移到节点 A。除非组 2 中的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务配置为不影响资源组中的其他服务，否则，当正在故障转移的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务失败时，正在故障转移到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务也将失败。  
  
## <a name="related-tasks"></a>Related Tasks  
 有关在群集中配置 Integration Services 服务的分步说明，请参阅 [将 Integration Services 服务配置为群集资源](../configure-the-integration-services-service-as-a-cluster-resource.md)。  
  
  
