---
title: "报表服务器应用程序的应用程序域 |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application domains [Reporting Services]
- recycling application domains
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0cec89b68c69b5e5ae6875d5d5d5e721008844cd
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="application-domains-for-report-server-applications"></a>报表服务器应用程序的应用程序域
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，报表服务器作为一个包含报表服务器 Web 服务、报表管理器和后台处理应用程序的服务来实现。 每个应用程序都在单个报表服务器进程中其各自的应用程序域中运行。 在大多数情况下，应用程序域是在内部创建、配置和管理的。 但是，如果要研究性能或内存问题并排除服务中断故障，则了解如何针对报表服务器应用程序域执行回收操作会非常有帮助。  
  
> [!NOTE]  
>  如果对使用基本身份验证的报表服务器配置报表生成器访问，则报表生成器将在其自己的应用程序域中运行。 此应用程序域与服务器进程中运行的其他应用程序域不同。 它由服务控制器进行管理，并且不受内存管理功能的限制，这些功能会为响应报表服务器上的内存不足而重新调整内存分配。  
  
 下面列出了可能会导致针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序执行应用程序域回收操作的事件：  
  
-   以预定义的时间间隔执行的计划回收操作。  
  
-   报表服务器上的配置更改。  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 配置更改。  
  
-   内存分配失败。  
  
 下表总结了为响应这些事件而发生的应用程序域回收行为：  
  
|事件|事件说明|适用于|可配置|回收操作说明|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|以预定义的时间间隔执行的计划回收操作|默认情况下，应用程序域每 12 个小时回收一次。<br /><br /> 对于提升了总体进程运行状况的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序来说，计划的回收操作是通常的做法。|报表服务器 Web 服务<br /><br /> 报表管理器<br /><br /> 后台处理应用程序|是。 RSReportServer.config 文件中的**RecycleTime** 配置设置可以确定回收时间间隔。<br /><br /> **MaxAppDomainUnloadTime** 设置了能够在其间完成后台处理的等待时间。|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 管理 Web 服务和报表管理器的回收操作。<br /><br /> 对于后台处理应用程序，报表服务器为那些从计划中启动的新作业创建一个新的应用程序域。 已在进行中的作业将能够在当前的应用程序域中完成，直到等待时间过期。|  
|报表服务器上的配置更改|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将为了响应 RSReportServer.config 文件中的更改而回收应用程序域。|报表服务器 Web 服务<br /><br /> 报表管理器<br /><br /> 后台处理应用程序|否。|您不能禁止执行回收操作。 但是，为了响应配置更改而执行的回收操作将按照与计划的回收操作相同的方式进行处理。 将为新请求创建新的应用程序域，而当前的请求和作业将在当前的应用程序域中完成。|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 配置更改|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 会回收应用程序域，前提是对其所监视的文件（例如，machine.config 文件、Web.config 文件和 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 程序文件）进行了更改。|报表服务器 Web 服务<br /><br /> 报表管理器|否。|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 对该操作进行管理。<br /><br /> 由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 启动的回收操作不会影响后台处理应用程序域。|  
|内存不足和内存分配失败|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR 将立即回收应用程序域。|报表服务器 Web 服务<br /><br /> 报表管理器<br /><br /> 后台处理应用程序|否。|在内存严重不足时，报表服务器将不接受当前应用程序域中的新请求。 在此期间，服务器将拒绝新请求，并且会出现 HTTP 503 错误。 除非卸载旧应用程序域，否则将不创建新应用程序域。 这意味着，如果您在服务器内存严重不足时对配置文件进行更改，则正在进行的请求和作业可能无法启动或完成。<br /><br /> 如果内存分配失败，则所有的应用程序域将立即重新启动。 正在进行的作业和请求将被放弃。 您必须手动重新启动这些作业和请求。|  
  
## <a name="planned-and-unplanned-recycle-operations"></a>计划内和计划外回收操作  
 根据导致回收操作的条件，回收操作可以是计划内操作或计划外操作：  
  
-   计划内回收操作按在 RSReportServer.config 文件中定义的固定时间间隔发生。 默认值为每 12 个小时。 对于提升了总体进程运行状况的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序来说，这是通常的做法。 对于计划内回收操作，报表服务器会为新请求创建其他应用程序域。 已在进行中的请求将能够在当前的应用程序域中完成，直到等待时间过期。 对于服务器来说，用来控制计划内回收操作的配置设置将作为一个整体来设置。 您无法为每个应用程序配置不同的回收计划或内存阈值。  
  
-   为了响应配置更改、内存不足和内存分配失败，随时都可能发生计划外回收操作：  
  
    -   对于配置更改，报表服务器将尝试使用软回收操作，即，将新请求重定向到应用程序域的新实例。 如果软回收失败，报表服务器将启动对应用程序域的硬回收，即，取消所有正在进行的请求、关闭当前的应用程序域并重新启动应用程序域。  
  
    -   内存分配失败是指系统资源对于服务器所执行的报表处理量来说不足。 所有应用程序域的硬回收操作都是为了响应内存分配失败而执行的。 所有的请求队列都将被清除。 已取消的请求将不会重新动。 正在以交互方式查看报表的用户必须刷新或重新打开报表。 计划的处理将在下一个预定时间发生。 如果无法接受这种延迟，则可以手动刷新报表快照，或者修改订阅计划或报表快照计划，以便它立即运行。  
  
 报表服务器 Web 服务、报表管理器和后台处理应用程序的应用程序域可以在一起回收，也可以单独回收，具体取决于导致进行回收的情况：  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 启动的回收操作只会影响 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序：报表服务器 Web 服务和报表管理器。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 将会根据其所监视的文件是否发生了更改来回收应用程序域。 由 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 启动的回收操作通常独立于后台处理应用程序的回收操作。  
  
-   由报表服务器执行的回收操作通常会影响报表服务器 Web 服务、报表管理器和后台处理应用程序。 回收操作是为了响应配置设置更改和服务重新启动而执行的。  
  
## <a name="rsreportserver-configuration-settings-for-application-domains"></a>应用程序域的 RSReportServer 配置设置  
 配置设置是在 [RSReportServer.config 文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)中指定的。 下面的示例演示了计划内应用程序域回收行为的默认配置设置。  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 下表对这些元素进行了说明。  
  
|元素|适用于|定义|  
|-------------|----------------|----------------|  
|**RecycleTime**|所有三个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序域|指定应用程序域的回收频率。 默认回收计划遵循通常用于 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序域回收的 12 小时制模式。 在计划的时间，所有的新请求都将转发到新的应用程序域实例。 原始实例中当前正在处理的请求能够完成。 一旦完成所有进程，就会删除原始实例，新的实例将成为唯一的活动应用程序域实例。<br /><br /> 默认值为 720 分钟。|  
|**MaxAppDomainUnloadTime**|仅限后台处理应用程序域|默认情况下，报表服务器分配的等待时间为 30 分钟，这是在回收操作期间允许应用程序域关闭的时间。 如果在所分配的时间内无法完成当前正在处理的作业（或者某个作业的所用时间比允许的等待时间长），则会立即重新启动应用程序域实例。 所有未完成的作业都将终止。<br /><br /> 有关如何查看状态或取消报表服务器上所运行作业的详细信息，请参阅[取消报表服务器作业 (Management Studio)](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)。|  
  
> [!NOTE]  
>  尽管报表服务器 Web 服务和报表管理器是 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序，但是，这两个应用程序都不响应可能已在 machine.config 中为 IIS 中所承载的 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序指定的计划应用程序域回收。  
  
## <a name="see-also"></a>另请参阅  
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [为报表服务器应用程序配置可用内存](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  
