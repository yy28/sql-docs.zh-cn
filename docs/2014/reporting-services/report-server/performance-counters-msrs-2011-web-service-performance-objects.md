---
title: MSRS 2014 Web Service 和 MSRS 2014 Windows Service 性能对象 （本机模式） 的性能计数器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- Report Server Web service, performance counters
- Reporting Services performance object
- RS Web Service performance object
- counters [Reporting Services]
- performance [Reporting Services]
ms.assetid: c642fc4f-8734-4626-a194-42ac9cd8e2ef
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a1fd420af1a50623f6f248e4dc99426907e987c4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365686"
---
# <a name="performance-counters-for-the-msrs-2014-web-service-and-msrs-2014-windows-service-performance-objects-native-mode"></a>MSRS 2014 Web Service 和 MSRS 2014 Windows Service 性能对象的性能计数器（本机模式）
  本主题介绍 `MSRS 2014 Web Service` 和 `MSRS 2014 Windows Service` 性能对象的性能计数器  
  
> [!NOTE]  
>  这些性能对象监视本地报表服务器上的事件。 如果是在扩展部署中运行报表服务器，则只对当前服务器（而不是扩展部署）进行计数。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式  
  
 Windows 性能监视器 (**Perfmon.exe**) 中提供了性能对象。 有关详细信息，请参阅 Windows 文档，[运行时分析](https://msdn.microsoft.com/library/w4bz2147.aspx) (https://msdn.microsoft.com/library/w4bz2147.aspx)。  
  
 有关与 SharePoint mode 性能计数器相关的信息，请参阅[MSRS 2014 Web Service SharePoint Mode 和 MSRS 2014 Windows Service SharePoint Mode 性能对象的性能计数器&#40;SharePoint 模式下&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md).  
  
 **本主题内容：**  
  
-   [MSRS 2014 Web Service 性能计数器](#bkmk_webservice)  
  
-   [MSRS 2014 Windows Service 性能计数器](#bkmk_windowsservice)  
  
-   [使用 PowerShell Cmdlet 返回列表](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> MSRS 2014 Web Service 性能计数器  
 `MSRS 2014 Web Service` 性能对象监视报表服务器性能。 此性能对象包括一系列用于跟踪报表服务器处理的计数器，这些处理通常通过交互式报表查看操作启动。 在设置计数器时，可将此计数器应用于 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的全部实例，也可以选择特定实例。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，这些计数器就会重置。  
  
 下表列出了 `MSRS 2014 Web Service` 性能对象中包含的计数器。  
  
|计数器|Description|  
|-------------|-----------------|  
|`Active Sessions`|活动会话的数目。 此计数器提供报表执行生成的所有浏览器会话的累积数，而不管这些会话是否仍处于活动状态。<br /><br /> 删除会话记录后，此计数器的计数即会相应减少。 默认情况下，如果会话在 10 分钟之内无任何活动，就会被删除。|  
|`Cache Hits/Sec`|每秒请求缓存报表的次数。 这些请求是对重新呈现的报表的请求，而不是对直接从缓存处理的报表的请求。 （请参阅本主题稍后部分中的 `Total Cache Hits`。）|  
|`Cache Hits/Sec (Semantic Models)`|每秒请求缓存模型的次数。 这些请求是对重新呈现的报表的请求，而不是对直接从缓存处理的报表的请求。|  
|`Cache Misses/Sec`|每秒未能从缓存返回报表的请求次数。 使用此计数器可以查明是否有足够的资源（磁盘或内存）用于缓存。|  
|`Cache Misses/Sec (Semantic Models)`|每秒未能从缓存返回模型的请求次数。 使用此计数器可以查明是否有足够的资源（磁盘或内存）用于缓存。|  
|`First Session Requests/Sec`|每秒从报表服务器缓存启动的新用户会话的数目。|  
|`Memory Cache Hits/Sec`|每秒从内存中缓存检索到报表的次数。 *内存中缓存* 是缓存的一部分，可将报表存储在 CPU 内存中。 使用内存中缓存时，报表服务器不会在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中查询缓存的内容。|  
|`Memory Cache Misses/Sec`|每秒从内存中缓存未检索到报表的次数。|  
|`Next Session Requests/Sec`|对当前会话中打开的报表（例如通过会话快照呈现的报表）的每秒请求数。|  
|`Report Requests`|当前处于活动状态且正由报表服务器管理的报表的数目。|  
|`Reports Executed/Sec`|每秒成功执行报表的次数。 此计数器提供有关报表量的统计信息。 将此计数器与 `Request/Sec` 一起使用，可以对报表执行与可以从缓存返回的报表请求进行比较。|  
|`Requests/Sec`|每秒向报表服务器发出的请求的次数。 此计数器可跟踪报表服务器管理的所有类型请求。|  
|`Total Cache Hits`|服务启动后请求缓存报表的总次数。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，此计数器就会重置。|  
|`Total Cache Hits (Semantic Models)`|服务启动后请求缓存中的模型的总次数。 只要 ASP.NET 停止报表服务器 Web 服务，此计数器就会重置。|  
|`Total Cache Misses`|服务启动后未能从缓存返回报表的总次数。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，此计数器就会重置。 使用此计数器可确定是否有足够的磁盘空间和内存。|  
|`Total Cache Misses (Semantic Models)`|服务启动后未能从缓存返回模型的总次数。 只要 ASP.NET 停止报表服务器 Web 服务，此计数器就会重置。 使用此计数器可确定是否有足够的磁盘空间和内存。|  
|`Total Memory Cache Hits`|服务启动后从内存中缓存返回的缓存报表的总数。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，此计数器就会重置。 *内存中缓存* 是缓存的一部分，可将报表存储在 CPU 内存中。 使用内存中缓存时，报表服务器不会在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中查询缓存的内容。|  
|`Total Memory Cache Misses`|服务启动后在内存中缓存的缓存失误总数。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，此计数器就会重置。|  
|`Total Processing Failures`|针对报表服务器 Web 服务的请求处理错误数。|  
|`Total Rejected Threads`|系统拒绝异步处理的总线程数，这些线程随后将以同一线程中同步进程的形式处理。 每个数据源在一个线程中进行处理。 如果线程量超出了系统容量，系统将拒绝对线程进行异步处理，随后会按串行方式处理。|  
|`Total Reports Executed`|服务启动后成功运行的报表的总数。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，此计数器就会重置。|  
|`Total Requests`|服务启动后对报表服务器发出的全部请求的总数。 只要 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 停止报表服务器 Web 服务，此计数器就会重置。|  
  
##  <a name="bkmk_windowsservice"></a> MSRS 2014 Windows Service 性能计数器  
 `MSRS 2014 Windows Service` 性能对象监视报表服务器 Windows 服务。 此性能对象包括一系列用于跟踪报表处理的计数器，这些处理通过计划操作启动。 计划操作可以包括订阅和传递、报表执行快照和报表历史记录。 在设置计数器时，可将此计数器应用于 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的全部实例，也可以选择特定实例。  
  
 下表列出了 `MSRS 2014 Windows Service` 性能对象中包含的计数器。  
  
|计数器|Description|  
|-------------|-----------------|  
|`Active Sessions`|存储在报表服务器数据库中的活动会话数。 此计数器提供报表订阅生成的所有可用浏览器会话的累积数，而不管这些会话是否仍处于活动状态。|  
|`Cache Flushes/Sec`|每秒刷新的缓存数。|  
|`Cache Hits/Sec`|每秒请求缓存报表的次数。 这些请求是对重新呈现的报表的请求，而不是对直接从缓存处理的报表的请求。 （请参阅本主题稍后部分中的 `Total Cache Hits`。）|  
|`Cache Hits/Sec (Semantic Models)`|每秒请求缓存模型的次数。|  
|`Cache Misses/Sec`|每秒未能从缓存返回报表的请求次数。 使用此计数器可以查明是否有足够的资源（磁盘或内存）用于缓存。|  
|`Cache Misses/Sec (Semantic Models)`|每秒未能从缓存返回模型的请求次数。 使用此计数器可以查明是否有足够的资源（磁盘或内存）用于缓存。|  
|`Delivers/Sec`|所有传递扩展插件每秒进行报表传递的次数。|  
|`Events/Sec`|每秒处理的事件数。 监视的事件包括 `SnapshotUpdated` 和 `TimedSubscription`。|  
|`First Session Requests/Sec`|每秒创建的新报表执行会话的数目。|  
|`Memory Cache Hits/Sec`|每秒从内存中缓存检索到报表的次数。 *内存中缓存* 是缓存的一部分，可将报表存储在 CPU 内存中。 使用内存中缓存时，报表服务器不会在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中查询缓存的内容。|  
|`Memory Cache Misses/Sec`|每秒从内存中缓存未检索到报表的次数。|  
|`Next Session Requests/Sec`|对当前会话中打开的报表（例如通过会话快照呈现的报表）的每秒请求数。|  
|`Report Requests`|当前处于活动状态且正由报表服务器管理的报表的数目。 使用此计数器可以评估缓存策略。 请求数可能会比报表生成的请求数更多。|  
|`Reports Executed/Sec`|每秒成功生成的报表数。|  
|`Requests/Sec`|报表服务器服务每秒处理的成功请求的总数。|  
|`Snapshot Updates/Sec`|每秒报表执行快照更新的总数。|  
|`Total App Domain Recycles`|报表服务器 Windows 服务启动后应用程序域循环的总次数。|  
|**总缓存刷新数**|服务启动后报表服务器缓存更新的总次数。 当应用程序域回收时，将重置此计数器。 请参阅 `Cache Flushes/Sec`。|  
|`Total Cache Hits`|报表服务器 Windows 服务启动后请求直接从缓存处理的报表的总次数。 当应用程序域回收时，将重置此计数器。 请参阅 `Cache Hits/Sec`。|  
|`Total Cache Hits (Semantic Models)`|报表服务器 Windows 服务启动后请求直接从缓存处理模型的总次数。 当应用程序域回收时，将重置此计数器。 请参阅 `Cache Hits/Sec`。|  
|`Total Cache Misses`|报表服务器 Windows 服务启动后报表未能从缓存返回的总次数。 当应用程序域回收时，将重置此计数器。 请参阅 `Cache Misses/Sec`。|  
|`Total Cache Misses (Semantic Models)`|报表服务器 Windows 服务启动后模型未能从缓存返回的总次数。 当应用程序域回收时，将重置此计数器。|  
|`Total Deliveries`|对于所有传递扩展插件，通过计划和传递处理器所传递的报表总数。 当应用程序域回收时，将重置此计数器。|  
|`Total Events`|报表服务器 Windows 服务启动后发生的事件总数。 当应用程序域回收时，将重置此计数器。|  
|`Total Memory Cache Hits`|报表服务器 Windows 服务启动后从内存中缓存返回的缓存报表总数。 当应用程序域回收时，将重置此计数器。|  
|`Total Memory Cache Misses`|服务启动后在内存中缓存的缓存失误总数。 当应用程序域回收时，将重置此计数器。|  
|`Total Processing Failures`|报表服务器 Windows 服务中的请求处理错误数。|  
|`Total Rejected Threads`|系统拒绝异步处理的总线程数，这些线程随后将以同一线程中同步进程的形式处理。 在中等或高负载下，该计数器将稳定增长。|  
|`Total Reports Executed`|运行报表的总数。|  
|`Total Requests`|服务启动后成功运行的报表的总数。 当应用程序域回收时，将重置此计数器。|  
|`Total Snapshot Updates`|报表执行快照更新的总数|  
  
##  <a name="bkmk_powershell"></a> 使用 PowerShell Cmdlet 返回列表  
 ![与 PowerShell 相关的内容](../media/rs-powershellicon.jpg "PowerShell related content")下面的 Windows PowerShell 脚本将返回 CounterSetName 以“msr”开头的计数器集：  
  
```  
get-counter -listset msr*  
```  
  
 下面的 Windows PowerShell 脚本将返回 CounterSetName 的性能计数器列表。  
  
```  
(get-counter -listset "MSRS 2014 Windows Service").paths  
```  
  
## <a name="see-also"></a>请参阅  
 [监视报表服务器性能](monitoring-report-server-performance.md)   
 [MSRS 2014 Windows Service SharePoint Mode 性能对象和 MSRS 2014 Web Service SharePoint Mode 性能计数器&#40;SharePoint 模式&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [ReportServer:Service 和 ReportServerSharePoint:Service 性能对象的性能计数器](performance-counters-reportserver-service-performance-objects.md)  
  
  
