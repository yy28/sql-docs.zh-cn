---
title: "R 服务的资源调控 | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# R 服务的资源调控
  使用 R 的一个难点是分析大量的数据在生产中不需要其他硬件和数据通常转为数据库外部的计算机不受 IT。  若要执行高级分析功能操作时，客户想要利用数据库的服务器资源，并且要保护他们的数据，它们需要这种操作都符合企业级法规遵从性要求，如安全性和性能。  
  
 本部分提供有关如何管理由 R 运行时和运行时使用的 R 作业所使用的资源信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与计算上下文的实例。  
  
## 什么是对资源进行监管？  
 对资源进行监管旨在识别并防止在数据库服务器环境中，其中通常有多个从属应用程序和多个服务以支持并平衡中很常见的问题。 有关 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，资源调控涉及以下任务︰  
  
-   标识使用过多的服务器资源的脚本。  
  
     管理员需要能够终止或进行遏制消耗过多的资源的作业。  
  
-   缓解不可预测的工作负荷。  
  
     例如，如果在服务器上同时运行多个 R 作业和作业不是相互隔离的通过使用资源池，产生的资源争用可能导致不可预知的性能或威胁的工作负荷完成。  
  
-   确定优先级的工作负荷。  
  
     管理员或架构师必须是能够指定工作负荷，必须更高的优先级，或确保某些工作负荷完成如果资源的争用。  
  
 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，您可以使用 [资源调控器](../../relational-databases/resource-governor/resource-governor.md) 来管理由 R 运行时和远程 R 作业所使用的资源。  
  
## 为使用资源调控器如何管理 R 作业  
 一般情况下，您管理资源分配给 R 作业通过创建 *外部的资源池* 并将工作负荷分配到池或池。 外部资源池是一种新的资源库中引入 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，以帮助管理 R 运行时和外部数据库引擎的其他进程。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，现在有三种类型的默认资源池。  
  
-    *内部池* 表示资源使用的 SQL Server 本身并不能进行更改或限制。  
  
-    *默认池* 是可用于修改服务器作为一个整体的资源使用的预定义的用户池。 此外可以定义属于此池来管理对资源的访问的用户组。  
  
-    *默认外部池* 是用于外部资源的预定义的用户池。 此外，可以创建新的外部资源池，并定义用于属于此池的用户组。  
  
 此外，您可以创建 *用户定义的资源池* 分配的资源添加到数据库引擎或其他应用程序，并创建 *用户定义的外部资源池* R 和其他外部进程管理。  
  
 详细介绍了术语和一般概念，请参阅 [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。  
  
> [!NOTE]  
>  新的资源调控器属性目前仅通过 DDL 语句或脚本;不能使用中的用户界面创建外部资源组 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
## 使用资源调控器资源管理 

   如果您是新于资源调控器，请参阅本主题有关如何修改实例默认资源，并且创建新的外部资源池的快速演练︰  [How To︰ 为 R 创建资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 您可以使用 *外部的资源池* 的机制来管理使用以下 R 可执行文件的资源︰  
  
-   Rterm.exe 和附属过程  
  
-   BxlServer.exe 和附属过程  
  
-   通过快速启动板启动的附属进程  
  
 但是，不支持的直接管理的快速启动板服务通过使用资源调控器。 这是因为 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是设计使然可以受信任的服务承载由 Microsoft 提供的启动器。 受信任的启动器也配置为避免占用过多的资源。  
  
 我们建议您管理使用资源调控器的附属进程和调整它们以满足每个数据库配置和工作负荷的需求。  例如，可以创建或销毁按需在执行期间各附属的任何进程。  
  
## 禁用外部脚本执行  
 支持外部脚本是可选的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。 在安装后 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], 、 执行外部脚本的功能默认情况下，为 OFF，您必须手动重新配置该属性并重新启动实例后，若要启用脚本执行。  
  
 因此，如果没有立即，缓解所需要的资源问题或安全问题，管理员可以立即禁用任何外部脚本执行使用 [sp_configure & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 并设置属性 `external scripts enabled` 为 FALSE，则为 0。  
  
## 另请参阅  
 [管理和监视 R 解决方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [如何︰ 为 R 创建资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  