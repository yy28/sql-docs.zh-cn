---
title: 为报表服务器应用程序配置可用内存 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- memory [Reporting Services]
- memory thresholds [Reporting Services]
ms.assetid: ac7ab037-300c-499d-89d4-756f8d8e99f6
caps.latest.revision: 49
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6958198b0482c792a952efea5c3792a182df8564
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198272"
---
# <a name="configure-available-memory-for-report-server-applications"></a>为报表服务器应用程序配置可用内存
  尽管 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 可使用所有可用内存，但您可以通过为分配给 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 服务器应用程序的内存资源总量配置上限来覆盖默认行为。 此外，您还可以设置阈值，以便报表服务器根据内存压力（低、中或高）来更改其排列请求优先级和处理请求的方式。 在内存压力较低时，报表服务器通过为交互式或按需报表处理提供一个略高的优先级进行响应。 在内存压力较高时，报表服务器使用多种方法在可用资源有限的情况下保持运行状态。  
  
 本主题介绍用户可以指定的配置设置，还说明了服务器在内存压力成为处理请求的决定因素时的响应方式。  
  
## <a name="memory-management-policies"></a>内存管理策略  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 通过调整分配给特定的应用程序和特定类型的处理请求的内存量来响应系统资源约束。 在报表服务器服务中运行和受内存管理限制的应用程序包括：  
  
-   报表管理器，一个用于报表服务器的 Web 前端应用程序。  
  
-   报表服务器 Web 服务，用于交互式报表处理和按需请求。  
  
-   后台处理应用程序，用于计划的报表处理、订阅传递和数据库维护。  
  
 内存管理策略适用于整个报表服务器服务，而不适用于进程中运行的单个应用程序。  
  
 如果系统没有内存压力，则每个服务器应用程序在启动时（收到请求前）都会请求一些内存，以便在最终收到请求时提供最优性能。 当产生内存压力时，报表服务器就会调整其进程模型，如下表中所述。  
  
|内存压力|服务器响应|  
|---------------------|---------------------|  
|Low|继续处理当前请求。 几乎总是接受新请求。 定向到后台处理应用程序的请求优先级低于定向到报表服务器 Web 服务的请求优先级。|  
|Medium|继续处理当前请求。 可能会接受新请求。 定向到后台处理应用程序的请求优先级低于定向到报表服务器 Web 服务的请求优先级。 所有三种服务器应用程序的内存分配都将减少，但后台处理应用程序的内存减少相对更多，以便为 Web 服务器请求提供更多可用内存。|  
|High|进一步减少内存分配。 拒绝要请求更多内存的服务器应用程序。 当前请求的速度将会降低，完成所需的时间会更长。 不接受新请求。 报表服务器将内存中的数据文件交换到磁盘。<br /><br /> 如果内存约束很严格，因此没有可用于处理新请求的内存，则报表服务器将在完成当前请求时返回 HTTP 503 服务器不可用的错误。 在某些情况下，可以回收应用程序域以立即减少内存压力。|  
  
 尽管无法对不同内存压力情况自定义报表服务器响应，但您可以指定配置设置，以定义区分高、中和低内存压力响应的边界。  
  
## <a name="when-to-customize-memory-management-settings"></a>何时自定义内存管理设置  
 默认设置为低、中和高内存压力指定了不同的范围。 默认情况下，低内存压力区域大于中内存压力和高内存压力区域。 此配置最适于处理平均分发或增量增加或减少的负载。 在这种情况下，各区域之间的切换是渐进的，因此报表服务器有时间调整其响应。  
  
 如果负载模式包含峰值，修改默认设置将非常有用。 当处理负荷中突然出现峰值时，报表服务器可能会迅速从无内存压力状态转为内存分配失败状态。 如果您同时启动了某个占用大量内存的报表的多个并发实例，则可能会发生这种情况。 若要处理此类型的处理负荷，需要将报表服务器尽可能移动到中或高内存压力响应中，以便降低处理速度。 这样可以完成更多的请求。 为此，您应该降低 `MemorySafetyMargin` 的值，使低内存压力区域相对于其他区域更小。 此操作将导致对中内存压力和高内存压力的响应更早发生。  
  
## <a name="configuration-settings-for-memory-management"></a>内存管理的配置设置  
 控制报表服务器的内存分配的配置设置包括`WorkingSetMaximum`， `WorkingSetMinimum`， `MemorySafetyMargin`，和`MemoryThreshold`。  
  
-   `WorkingSetMaximum` 和`WorkingSetMinimum`定义可用内存的范围。 您可以配置这些设置，以便为报表服务器应用程序设置可用内存范围。 如果要在同一台计算机上承载多个应用程序，并且确定报表服务器相对于同一台计算机上的其他应用程序消耗的系统资源过多，则此设置可能很有用。  
  
-   `MemorySafetyMargin` 和`MemoryThreshold`设置低、 中和高级别的内存压力的边界。 每种状态[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]都会采取纠正操作，以确保报表处理和其他请求能够得到正确处理相对于计算机可用的内存量。 您可以指定配置设置以确定低、中和高压力级别之间的说明。  
  
     尽管您可以更改配置设置，但这样不会提高报表处理性能。 仅当请求在完成之前被删除时，更改配置设置才有用。 提高服务器性能的最佳方法是在专用计算机上部署报表服务器或单个报表服务器应用程序。  
  
 下图显示了如何综合使用这些设置来区分低、中和高级别的内存压力：  
  
 ![内存状态的配置设置](../media/rs-memoryconfigurationzones.gif "Configuration settings for memory state")  
  
 下表描述了`WorkingSetMaximum`， `WorkingSetMinimum`， `MemorySafetyMargin`，和`MemoryThreshold`设置。 配置设置中指定[RSReportServer.config 文件](rsreportserver-config-configuration-file.md)。  
  
|元素|Description|  
|-------------|-----------------|  
|`WorkingSetMaximum`|指定内存阈值，在超出此值后将不会向报表服务器应用程序授予任何新的内存分配请求。<br /><br /> 默认情况下，报表服务器将 `WorkingSetMaximum` 设置为计算机上的可用内存量。 启动服务时，将会检测此值。<br /><br /> 除非您手动添加，否则此设置不会显示在 RSReportServer.config 文件中。 如果希望报表服务器使用较少的内存，则可修改 RSReportServer.config 文件并添加该元素和值。 有效值的范围为 0 到最大整数之间。 此值以 KB 为单位表示。<br /><br /> 达到 `WorkingSetMaximum` 的值时，报表服务器将不接受新请求。 允许完成当前正在执行的请求。 仅当用内存低于通过指定的值时，才会接受新请求`WorkingSetMaximum`。<br /><br /> 如果现有请求继续占用额外内存后的`WorkingSetMaximum`达到值，将回收所有报表服务器应用程序域。 有关详细信息，请参阅 [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md)。|  
|`WorkingSetMinimum`|指定资源占用的下限；如果内存使用总量低于此限制值，报表服务器将不会释放内存。<br /><br /> 默认情况下，将在服务启动时计算该值。 计算结果为初始内存分配请求占 `WorkingSetMaximum` 的 60%。<br /><br /> 除非您手动添加，否则此设置不会显示在 RSReportServer.config 文件中。 如果你想要自定义此值，则必须添加`WorkingSetMinimum`到 RSReportServer.config 文件的元素。 有效值的范围为 0 到最大整数之间。 此值以 KB 为单位表示。|  
|`MemoryThreshold`|指定的百分比`WorkingSetMaximum`用于定义高和中等压力方案之间的边界。 如果报表服务器内存使用情况达到此值，报表服务器将降低请求处理速度，并更改分配给其他服务器应用程序的内存量。 默认值为 90。 此值应大于为设置的值`MemorySafetyMargin`。|  
|`MemorySafetyMargin`|指定 `WorkingSetMaximum` 的百分比，该百分比用于定义中压情况和低压情况之间的边界。 此值是为系统保留的可用内存百分比，无法用于报表服务器操作。 默认值为 80。|  
  
> [!NOTE]  
>  `MemoryLimit` 和 `MaximumMemoryLimit` 设置在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中已过时。 如果升级现有安装或使用包含这些设置的 RSReportServer.config 文件，报表服务器将不再读取这些值。  
  
#### <a name="example-of-memory-configuration-settings"></a>内存配置设置示例  
 下面的示例显示了使用自定义内存配置值的报表服务器计算机的配置设置。 如果你想要添加`WorkingSetMaximum`或`WorkingSetMinimum`，必须在 RSReportServer.config 文件中键入这些元素和值。 两个值都是整数，表示要分配给服务器应用程序的 RAM（以 KB 为单位）。 下面的示例指定报表服务器应用程序的总内存分配不能超过 4 GB。 如果 `WorkingSetMinimum` 的默认值（`WorkingSetMaximum` 的 60%）是可以接受的，则可忽略该值并在 RSReportServer.config 文件中仅指定 `WorkingSetMaximum`。 此示例包括 `WorkingSetMinimum` 以说明在要添加该元素时的显示方式：  
  
```  
      <MemorySafetyMargin>80</MemorySafetyMargin>  
      <MemoryThreshold>90</MemoryThreshold>  
      <WorkingSetMaximum>4000000</WorkingSetMaximum>  
      <WorkingSetMinimum>2400000</WorkingSetMinimum>  
```  
  
#### <a name="about-aspnet-memory-configuration-settings"></a>关于 ASP.NET 内存配置设置  
 尽管报表服务器 Web 服务和报表管理器是[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]应用程序，两个应用程序中指定的内存配置设置会响应`processModel`一部分针对的 machine.config[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]应用程序，在 IIS 5.0 兼容性模式下运行。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 从 RSReportServer.config 文件中读取内存配置设置。  
  
## <a name="see-also"></a>请参阅  
 [RSReportServer 配置文件](rsreportserver-config-configuration-file.md)   
 [RSReportServer 配置文件](rsreportserver-config-configuration-file.md)   
 [修改 Reporting Services 配置文件 (RSreportserver.config)](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [报表服务器应用程序的应用程序域](application-domains-for-report-server-applications.md)  
  
  
