---
title: "R Services 的资源调控 | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5475c2258971c48c2e19bba69d9ec962ae48be87
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-r-services"></a>R Services 的资源调控
  使用 R 的一个难点在于，在生产环境中分析大量数据需要额外的硬件，并且通常要将数据从数据库移到不受 IT 控制的计算机。  若要执行高级分析操作，客户需要利用数据库服务器资源；若要保护数据，他们需要此类操作符合企业级合规要求，例如安全性和性能方面的要求。  
  
 本部分介绍如何管理 R 运行时使用的，以及在将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例用作计算上下文的情况下运行的 R 作业使用的资源。  
  
## <a name="what-is-resource-governance"></a>什么是资源调控？  
 资源调控旨在识别和防范数据库服务器环境中的常见问题。这种环境通常包含多个要支持和平衡的依赖应用程序与服务。 对于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，资源调控涉及到以下任务：  
  
-   识别使用过多服务器资源的脚本。  
  
     管理员需要能够终止或限制消耗过多资源的作业。  
  
-   消减不可预测的工作负荷。  
  
     例如，如果多个 R 作业在服务器上并行运行，并且未使用资源池将这些作业彼此隔离，则产生的资源争用可能会导致性能不可预测，或者影响工作负荷的完成。  
  
-   排定工作负荷的优先级。  
  
     管理员或架构师需要能够指定必须优先处理的工作负荷，或者保证在出现资源争用时能够完成某些工作负荷。  
  
 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，可以使用[资源调控器](../../relational-databases/resource-governor/resource-governor.md)来管理 R 运行时和远程 R 作业所用的资源。  
  
## <a name="how-to-use-resource-governor-to-manage-r-jobs"></a>如何使用资源调控器管理 R 作业  
 一般情况下，可以通过创建*外部资源池*并将工作负荷分配到一个或多个池，来管理分配给 R 作业的资源。 外部资源池是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中引入的一种新型资源池，可帮助管理 R 运行时以及数据库引擎外部的其他进程。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，现在有三种类型的默认资源池。  
  
-   *内部池*表示 SQL Server 本身使用的、不可更改或限制的资源。  
  
-   *默认池*是预定义的用户池，可用于修改整个服务器的资源用量。 还可以定义属于此池的用户组，以管理对资源的访问。  
  
-   *默认外部池*是外部资源的预定义用户池。 此外，可以创建新的外部资源池，并定义属于此池的用户组。  
  
 还可以创建*用户定义的资源池*将资源分配到数据库引擎或其他应用程序，创建*用户定义的外部资源池*来管理 R 和其他外部进程。  
  
 有关术语和一般概念的全面介绍，请参阅[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。  

  
## <a name="resource-management-using-resource-governor"></a>使用资源调控器进行资源管理 

   如果你不熟悉资源调控器，请参阅以下主题，获取有关如何修改实例默认资源和新建外部资源池的快速演练：[如何为 R 创建资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 可以使用*外部资源池*机制来管理以下 R 可执行文件使用的资源：  
  
-   Rterm.exe 和附属进程  
  
-   BxlServer.exe 和附属进程  
  
-   LaunchPad 启动的附属进程  
  
 但是，不支持使用资源调控器直接管理 Launchpad 服务。 这是因为 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是一个受信任的服务，在设计上只能托管 Microsoft 提供的启动器。 此外，受信任的启动器已配置为避免消耗过多的资源。  
  
 我们建议使用资源调控器管理附属进程，并根据单个数据库配置和工作负荷的需求优化这些进程。  例如，在执行过程中，可以根据需要创建或销毁任一附属进程。  
  
## <a name="disable-external-script-execution"></a>禁用外部脚本执行  
 在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 过程中，对外部脚本的支持是可选的。 安装 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 后，执行外部脚本的功能默认已关闭，必须手动重新配置该属性并重新启动实例才能启用脚本执行。  
  
 因此，如果需要立即缓解某个资源问题或者出现了安全问题，管理员可以使用 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 并将属性 `external scripts enabled` 设置为 FALSE 或 0，来立即禁用任何外部脚本执行。  
  
## <a name="see-also"></a>另请参阅  
 [管理和监视 R 解决方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [如何为 R 创建资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  


