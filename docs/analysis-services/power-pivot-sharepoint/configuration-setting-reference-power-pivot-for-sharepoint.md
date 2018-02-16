---
title: "配置设置参考 (Power Pivot for SharePoint) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b57dd3f-7820-4ba8-b233-01dc68908273
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b66f1bb71a185be8663e1fab732a208a0ca99d87
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="configuration-setting-reference-power-pivot-for-sharepoint"></a>配置设置参考 (Power Pivot for SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
本主题提供有关 SharePoint 场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序使用的配置设置的参考文档。 如果您使用 PowerShell 脚本来配置服务器，或如果您要查找特定设置的信息，则本主题中的信息可提供详细的说明。  
  
 配置设置是针对每个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序进行设置的。 在场中，可以创建多个服务应用程序，从而配置同一物理服务实例的独立逻辑实例。 配置设置存储在为你配置的每个服务应用程序创建的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 应用程序数据库中。  
  
 如果您更改配置设置，则所做的更改立即生效并用于后续请求和连接。 正在进行的操作由在操作开始时起作用的设置控制。  
  
 单击下面的链接可阅读特定的配置部分：  
  
 [数据加载超时](#LoadingData)  
  
 [连接池](#ConnectionPool)  
  
 [负载平衡](#AllocationScheme)  
  
 [数据刷新](#DataRefresh)  
  
 [使用情况数据收集](#UsageData)  
  
 有关如何创建 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的说明，请参阅 [在管理中心中创建和配置 PowerPivot 服务应用程序](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)。  
  
##  <a name="LoadingData"></a> 数据加载超时  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据由场中的 Analysis Services 服务器实例检索并加载。 可以从内容库或从本地文件缓存加载数据，具体取决于上次访问数据的方式和时间。 只要收到查询或处理请求，就会将数据加载到内存中。 若要最大限度地提高服务器的总体可用性，您可以设置一个超时值以指示服务器在分配的时间内无法完成加载时停止数据加载请求。  
  
|名称|默认|有效值|Description|  
|----------|-------------|------------------|-----------------|  
|数据加载超时|1800（以秒为单位）|1 到 3600|指定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序等待来自特定 Analysis Services 服务器实例的响应的时长。<br /><br /> 默认情况下，当服务应用程序向引擎服务实例转发特定请求后，它将等待 30 分钟以便从该实例获得数据负载。<br /><br /> 如果在此时段内无法加载 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源，该线程将停止，并将启动一个新进程。|  
  
##  <a name="ConnectionPool"></a> 连接池  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序创建并管理连接池，以便重复使用连接。 连接池有两种类型：一种用于与只读数据建立数据连接；另一种用于建立服务器连接。  
  
 数据连接池包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源的缓存连接。 每个连接池都基于在加载数据库时设置的上下文。 此上下文包括物理服务实例的标识、数据库 ID 和请求数据的 SharePoint 用户的标识。 将为每个组合创建一个单独的连接池。 例如，来自在同一个服务器上运行的同一数据库的不同用户的请求将使用不同池中的连接。  
  
 连接池的作用是为同一 SharePoint 用户对于同一个 Analysis Services 数据库的只读请求使用缓存连接。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务实例是已在内存中加载了数据的服务器。 数据库 ID 是数据模型的内存中数据结构的内部标识符（模型实例化为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维数据集数据库）。 版本信息隐式包含在该标识符中。  
  
 服务器连接池包含从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序实例到 Analysis Services 服务器实例的缓存连接，其中，服务应用程序使用 Analysis Services 服务器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Sysadmin 权限进行连接。 这些连接用来发出加载数据库请求并监视系统运行状况。  
  
 每种连接池类型都有上限，您可以设置此上限，以确保以最佳方式将系统内存用于连接管理。  
  
|名称|默认|有效值|Description|  
|----------|-------------|------------------|-----------------|  
|连接池超时|1800（以秒为单位）|1 到 3600。|此设置适用于数据连接池。<br /><br /> 它指定空闲连接在被删除之前可以在连接池中保留多长时间。<br /><br /> 默认情况下，如果某个连接处于非活动状态超过五分钟，服务应用程序将删除此连接。|  
|最大用户连接池大小|1000|-1、0 或 1 到 10000。<br /><br /> -1 指定空闲连接数量不受限制。<br /><br /> 0 表示不保持空闲连接。 每次必须创建到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源的新连接。|此设置适用于为特定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序实例创建的所有数据连接池中的空闲连接数。<br /><br /> 将为 SharePoint 用户、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据和服务实例的唯一组合创建单个连接池。 如果你有许多用户访问各种 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源，服务器性能可能会因连接池大小的增加而受益。<br /><br /> 如果与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务实例的空闲连接数目超过 100 个，将断开最新的空闲连接，而不是将其返回到池中。|  
|最大管理连接池大小|200|-1、0 或 1 到 10000。<br /><br /> -1 指定空闲连接数量不受限制。|为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序与 Analysis Services 服务器实例之间的连接创建的所有管理连接池中的最大空闲服务器连接数目。 服务器连接用于请求加载数据库以及将更改保存回 SharePoint 数据库。|  
  
##  <a name="AllocationScheme"></a> 负载平衡  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务执行的功能之一是确定在可用的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务实例之间加载 Analysis Services 数据的位置。 **AllocationMethod** 设置指定选择服务实例时所依据的条件。  
  
|名称|默认|有效值|Description|  
|----------|-------------|------------------|-----------------|  
|分配方法|循环|循环<br /><br /> 基于运行状况|用于在两个或更多 Analysis Services 服务器实例之间分配负载请求的方案。<br /><br /> 默认情况下， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务将基于服务器运行状况平均分配请求。 “基于运行状况”选项基于可用内存和 CPU 利用率，将请求分配到具有最多可用系统资源的服务器。<br /><br /> 循环将按先后顺序在可用的服务器之间循环分配请求，而不考虑当前负载或服务器运行状况。|  
  
##  <a name="DataRefresh"></a> 数据刷新  
 指定为组织定义正常或典型工作日的小时数范围。 这些配置设置确定在工作时间后何时进行数据处理以便执行数据刷新操作。 工作时间后处理可在工作日结束时开始。 对于希望使用在正常工作时间内生成的事务数据来刷新 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源的文档所有者而言，工作时间后处理是一个计划选项。  
  
|名称|默认|有效值|Description|  
|----------|-------------|------------------|-----------------|  
|开始时间|上午 04:00|1 至 12 小时，其中，该值为此范围内的有效整数。<br /><br /> 类型为 Time。|设置工作时间范围的下限。|  
|结束时间|晚上 08:00|1 至 12 小时，其中，该值为此范围内的有效整数。<br /><br /> 类型为 Time。|设置工作时间范围的上限。|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 无人参与的数据刷新帐户|InclusionThresholdSetting|目标应用程序 ID|此帐户用于代表计划所有者运行数据刷新作业。<br /><br /> 无人参与的数据刷新帐户必须事先定义，然后才能在服务应用程序配置页中引用。 有关详细信息，请参阅 [配置 PowerPivot 无人参与的数据刷新帐户 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)。|  
|允许用户输入自定义 Windows 凭据|已启用|Boolean|确定计划的数据刷新配置页是否显示一个选项，让计划所有者能够指定用于运行数据刷新作业的 Windows 用户帐户和密码。<br /><br /> 必须启用安全存储区服务才能使用此选项。 有关详细信息，请参阅 [为 PowerPivot 数据刷新配置存储的凭据 (PowerPivot for SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)。|  
|最大处理历史记录长度|365|1 到 5000 天|确定数据刷新历史记录在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库中保留的时长。 有关详细信息，请参阅 [Power Pivot Usage Data Collection](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)。|  
  
##  <a name="UsageData"></a> 使用情况数据收集  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理仪表板中显示的使用情况报表可以提供有关如何使用启用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]的工作簿的重要信息。 针对以后在使用情况或活动报表中显示的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器事件，以下配置设置控制使用情况数据收集的各个方面。  
  
|名称|默认|有效值|Description|  
|----------|-------------|------------------|-----------------|  
|查询报告间隔|300（以秒为单位）|1 到 n 秒，其中 n 是任何有效的整数。|为了确保使用情况数据收集不消耗场的过多数据传输能力，将对每个连接收集查询统计信息并将其报告为单个事件。 “查询报告间隔”确定报告事件的频率。 默认情况下，每 5 分钟报告一次查询统计信息。<br /><br /> 因为只要发送请求就会立即关闭连接，所以，系统甚至会为访问单个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源的单个用户生成大量的连接。 因此，将为每个用户与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源组合创建连接池，以便在创建连接后，相同数据的同一用户可以重复使用此连接。 按照通过此配置设置指定的间隔， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序定期报告连接池中每个连接的使用情况数据。<br /><br /> 增加生成报表的时间值将导致记录较少的事件。 但是，如果将值设置得过高，当服务器重新启动或连接关闭时，就存在丢失事件数据的风险。<br /><br /> 降低此值将导致以更高的频率记录更多的事件，同时将更多与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]相关的使用情况数据添加到 SharePoint 使用情况数据库中的数据收集系统。<br /><br /> 一般而言，不要更改此配置设置，除非你试图解决特定问题（例如，如果使用情况数据库由于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 使用情况数据而增长过快）。|  
|使用情况数据历史记录|365（以天为单位）|0 或 1 到 n 天，其中 n 是任何有效的整数。<br /><br /> 0 意味着始终保留而不会删除历史记录。|默认情况下，使用情况数据在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库中保存一年时间。 早于一年前的记录将从数据库中删除。<br /><br /> 每天以及当运行 Microsoft SharePoint Foundation 使用情况数据处理作业时，将检查过期的历史数据。 该计时器作业将读取此设置，并对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库中过期的历史记录触发数据删除命令。|  
|一般响应上限|500（以毫秒为单位）|1 到 n 毫秒，其中 n 是任何有效的整数。|默认情况下，一般请求的阈值为半秒。<br /><br /> 一般请求包括服务器 ping、对元数据的请求和启动会话。|  
|快速响应上限|1000（以毫秒为单位）|1 到 n 毫秒，其中 n 是任何有效的整数。|默认情况下，快速请求的阈值为一秒。<br /><br /> 快速请求指的是具有极小数据集的请求，或针对涵盖大型成员集的元数据的请求。|  
|“预期响应上限”|3000（以毫秒为单位）|1 到 n 毫秒，其中 n 是任何有效的整数。|默认情况下，预期请求的阈值为三秒。<br /><br /> 此阈值设置预期查询时间的上限。|  
|长时间响应上限|10000（以毫秒为单位）|1 到 n 毫秒，其中 n 是任何有效的整数。|默认情况下，长请求的阈值为十秒。<br /><br /> 这些请求的运行时间比预期时间要长，但仍在可接受的范围内。|  
  
## <a name="see-also"></a>另请参阅  
 [在管理中心中创建和配置 PowerPivot 服务应用程序](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [使用 SharePoint 2010 进行 Power Pivot 数据刷新](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [配置使用情况数据收集 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [配置 Power Pivot 服务帐户](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Power Pivot 管理仪表板和使用情况数据](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
  
