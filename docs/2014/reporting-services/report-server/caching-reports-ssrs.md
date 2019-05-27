---
title: 缓存报表 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 58785d54954278d2dcb839ef3e707859682a9d37
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104113"
---
# <a name="caching-reports-ssrs"></a>缓存报表 (SSRS)
  报表服务器可以缓存已处理报表的副本，并在用户打开此报表时返回该副本。 对用户而言，可指示报表为缓存副本的唯一证据是报表的运行日期和时间。 如果日期或时间不是当前的日期或时间，并且报表不是快照，则说明该报表是从缓存中检索的。  
  
 在报表很大或需要频繁访问的情况下，缓存报表可以缩短检索该报表所需的时间。 如果重新启动服务器，则当报表服务器 Web 服务重新联机时，会恢复所有缓存的实例。  
  
 缓存是一种性能增强技术。 缓存的内容是非永久性的，会随着报表的添加、替换或删除而发生更改。 如果需要可预测性更高的缓存策略，则应创建报表快照。 有关详细信息，请参阅 [设置报表处理属性](set-report-processing-properties.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可以在数据库中存储临时文件以支持用户会话和报表处理。 缓存这些文件是为了供内部使用，以便在单一浏览器会话内保持一致的查看体验。 有关如何缓存内部使用的临时文件的详细信息，请参阅[报表服务器数据库（SSRS 本机模式）](report-server-database-ssrs-native-mode.md)。  
  
## <a name="cached-instances"></a>缓存实例  
 报表的缓存实例基于报表的中间格式。 报表服务器通常根据报表名称来缓存报表的单个实例。 但是，如果报表可以基于查询参数包含不同数据，则可以在任何给定的时间缓存该报表的多个版本。 例如，假设有一个参数化报表以区域代码作为参数值。 如果四个不同用户指定了四个唯一的区域代码，则将创建四个缓存副本。  
  
 用某个唯一区域代码运行报表的第一个用户将创建一个包含该区域的数据的缓存报表。 使用同一区域代码请求报表的后续用户将获取缓存副本。  
  
 并非所有报表都可以缓存。 如果报表包括用户相关数据，提示用户输入凭据或使用 Windows 身份验证，则不能缓存该报表。  
  
## <a name="refreshing-the-cache"></a>刷新缓存  
 如果用户在以前缓存的副本过期后选择该报表，则将使用更新的版本替换缓存报表。 配置为作为缓存实例运行的报表将根据过期设置按固定间隔从缓存中删除。 可以根据数据的即时性要求，以分钟为单位或按计划时间设置报表的过期时间。 除非使用 SOAP API，否则，不能直接从缓存中删除报表。  
  
 若要配置缓存过期时间，可以使用共享计划或报表特定计划。 如果使用共享计划，但随后又暂停了该计划，那么在计划暂停期间缓存不会过期。 如果后来删除了共享计划，该计划设置的副本将另存为报表特定计划。  
  
 如果计划过期，或者如果计划引擎在缓存过期的那一日不可用，则报表服务器在计划的操作恢复（通过延长计划或启动计划服务）之前将运行实时报表。  
  
## <a name="preloading-the-cache"></a>预加载缓存  
 为了提高服务器性能，可以预加载缓存。 可以通过两种方式使用一组参数化报表实例预加载缓存：  
  
1.  创建缓存刷新计划。 当您创建刷新计划时，可以为单个报表指定计划或指定共享计划。  
  
2.  创建使用 Null 传递提供程序的数据驱动订阅。 当将 Null 传递提供程序指定为订阅中的传递方法时，报表服务器会将报表服务器数据库当作传递目标，并使用称为空呈现扩展插件的专用呈现扩展插件。 与其他传递扩展插件相比，Null 传递提供程序没有可通过订阅定义配置的传递设置。  
  
 对于使用不同参数值生成不同报表实例的参数化报表，若要缓存该报表的多个实例，则更改报表将非常有用。 注意，只能对报表指定基于查询的参数。  
  
 当您指定计划或当您创建数据驱动订阅时，应安排向缓存传递报表的频率。 为了将新副本传递到缓存，旧副本必须已过期。 因此，必须对报表的执行属性进行配置以包括缓存过期设置。 过期设置必须与定义的订阅计划一致。 例如，如果创建一个每天晚上运行的订阅，则每天晚上在该订阅运行之前，缓存也应过期。 如果执行属性不包括过期时间，则将忽略后续的传递。 有关缓存刷新计划的详细信息，请参阅 [计划](../subscriptions/schedules.md)。 有关设置属性的详细信息，请参阅 [设置报表处理属性](set-report-processing-properties.md)。 有关使用数据驱动订阅的详细信息，请参阅 [数据驱动订阅](../subscriptions/data-driven-subscriptions.md)。  
  
## <a name="conditions-that-cause-cache-expiration"></a>导致缓存过期的条件  
 响应下列事件时会导致缓存报表失效：修改报表定义，修改报表参数，更改数据源凭据或者更改报表执行选项。 如果删除缓存中存储的报表，则也将删除该报表的缓存版本。  
  
 如果出于任何原因（例如，如果用户指定的参数值与生成缓存报表所用的参数值不同）无法从缓存实例呈现报表，则报表服务器将重新运行该报表。  
  
## <a name="see-also"></a>请参阅  
 [设置处理选项（SharePoint 集成模式下的 Reporting Services）](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [设置报表处理属性](set-report-processing-properties.md)   
 [Reporting Services 概念 (SSRS)](../reporting-services-concepts-ssrs.md)   
 [预加载缓存（报表管理器）](preload-the-cache-report-manager.md)   
 [“计划”](../subscriptions/schedules.md)   
 [缓存共享数据集 (SSRS)](cache-shared-datasets-ssrs.md)   
 [缓存刷新选项（报表管理器）](../cache-refresh-options-report-manager.md)  
  
  
