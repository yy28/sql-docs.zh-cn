---
title: 设置分区存储（Analysis Services 多维） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- low latency MOLAP
- standard storage [Analysis Services]
- hybrid OLAP
- automatic MOLAP
- relational OLAP
- multidimensional OLAP
- scheduled MOLAP [Analysis Services]
- partitions [Analysis Services], storage
- HOLAP
- MOLAP
- real time ROLAP
- real time HOLAP
- ROLAP
- medium latency MOLAP
ms.assetid: e525e708-f719-4905-a4cc-20f6a9a3edcd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d86734023080c9b7fc62cff636d4f1952d00d0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072993"
---
# <a name="set-partition-storage-analysis-services---multidimensional"></a>设置分区存储（Analysis Services - 多维）
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为存储模式和缓存选项提供了几种标准存储[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]配置。 它们为更新通知、滞后时间和重新生成数据提供了常用的配置。  
  
 您可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中多维数据集的“分区”选项卡中或在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的分区属性页面指定分区存储。  
  
## <a name="guidelines-for-choosing-a-storage-mode"></a>选择存储模式的准则  
 对于大型度量值组来说，为不同的分区配置不同的存储是常见的方法。 遵循以下指南：  
  
-   为不断发生更新的当前数据使用实时 ROLAP。  
  
-   基于不经常进行更新的数据源，为分区使用主动缓存和低滞后时间或中等滞后时间。  
  
-   为其用户需要高性能但能够承受一定的数据滞后时间的数据源使用自动 MOLAP。  
  
-   为其用户需要能够不断地访问数据但只是定期查看更改的数据源使用预定的 MOLAP。  
  
-   对不经常或根本不发生更改的分区、其用户不需要浏览最新数据的分区使用 MOLAP 存储，在任何必要的更新和处理期间数据对用户不必持续可用的情况下也使用 MOLAP 存储。  
  
 这些只是常规指南，您可能需要进行仔细的分析和测试来为您的数据开发最佳存储方案。 如果没有一种存储配置满足您的要求，您还可以手动为分区配置存储设置。  
  
## <a name="storage-settings-descriptions"></a>存储设置说明  
  
|标准存储设置|说明|  
|------------------------------|-----------------|  
|实时 ROLAP|OLAP 是实时的。 详细信息数据和聚合以关系格式存储。 当数据发生更改且所有查询都反映数据的当前状态时（零滞后时间），服务器侦听通知。<br /><br /> 通常将此设置用于经常不断地发生更新且其用户总是需要最新数据的数据源。 根据客户端应用程序生成的查询的类型，此方法可以保证提供最长的响应时间。|  
|实时 HOLAP|OLAP 是实时的。 详细信息数据以关系格式存储，而聚合以多维格式存储。 当数据发生更改并根据需要刷新多维 OLAP (MOLAP) 聚合时，服务器侦听通知。 不创建 MOLAP 缓存。 只要数据源发生了更新，服务器就切换到实时关系 OLAP (ROLAP) 直到聚合被刷新。 所有查询都反映数据的当前状态（零滞后时间）。<br /><br /> 通常将此设置用于经常不断地发生更新（但没有对实时 ROLAP 要求的那么频繁）且其用户总是需要最新数据的数据源。 一般情况下，此方法提供的总体性能要高于 ROLAP 存储。 如果数据源足够长时间地保持不变，则使用此设置的用户可以获得 MOLAP 般的性能。|  
|低滞后时间 MOLAP|详细信息数据和聚合均以多维格式存储。 在缓存中重新处理 MOLAP 对象时，服务器侦听数据的更改通知并切换到实时 ROLAP。 更新缓存之前需要至少 10 秒的静默间隔。 如果未达到静默间隔，将会有 10 分钟的覆盖间隔。 数据发生更改时处理自动进行，且目标滞后时间是首次更改后的 30 分钟。<br /><br /> 当查询性能比总是能够提供最新数据稍微重要时，通常将此设置用于经常发生更新的数据源。 在滞后间隔之后，此设置可随时按需要自动处理 MOLAP 对象。 重新处理 MOLAP 对象时，速度较慢。|  
|中等滞后时间 MOLAP|详细信息数据和聚合均以多维格式存储。 在缓存中重新处理 MOLAP 对象时，服务器侦听数据的更改通知并切换到实时 ROLAP。 更新缓存之前需要至少 10 秒的静默间隔。 如果未达到静默间隔，将会有 10 分钟的覆盖间隔。 数据发生更改时处理自动进行，且目标滞后时间为四小时。<br /><br /> 当查询性能比总是能够提供最新数据更重要时，通常将此设置用于经常（或不太经常）发生更新的数据源。 在滞后间隔之后，此设置可随时按需要自动处理 MOLAP 对象。 重新处理 MOLAP 对象时，速度较慢。|  
|自动 MOLAP|详细信息数据和聚合均以多维格式存储。 服务器侦听通知，但是在生成新的 MOLAP 缓存时保留当前的缓存。 生成新的缓存时，服务器切换到实时 OLAP，查询可能是陈旧的。<br /><br /> 创建新的 MOLAP 缓存之前，至少需要 10 秒的静默间隔。 如果未达到静默间隔，将会有 10 分钟的覆盖间隔。 数据发生更改时处理自动进行，且目标滞后时间为两小时。<br /><br /> 当查询性能非常重要时，此设置通常用于数据源。 在滞后间隔之后，此设置可随时按需要自动处理 MOLAP 对象。 生成和处理新缓存时查询不会返回最新数据。|  
|预定的 MOLAP|详细信息数据和聚合以多维格式存储。 如果数据发生更改，服务器将不会收到通知。 处理每隔 24 小时自动进行一次。<br /><br /> 通常将此设置用于只需要每天更新的数据源。 查询总是针对 MOLAP 缓存中的数据进行的，在新的缓存生成及其对象被处理之前，这些数据不会被放弃。|  
|MOLAP|不启用主动缓存。 详细信息数据和聚合均以多维格式存储。 如果数据发生更改，服务器将不会收到通知。 必须对处理进行预定，或者手动执行它。<br /><br /> 如果数据源中的定期更新对客户端程序来说不是必要的但高性能对其来说很关键，则通常为数据源使用此设置。<br /><br /> 如果应用程序不需要最新的数据，则不使用主动缓存的 MOLAP 会提供最佳性能。 尽管可以通过在临时服务器上更新和处理多维数据集及使用数据库同步将更新的和已处理的 MOLAP 对象复制到生产服务器上等方法来最大限度地减少停机时间，但是它的确需要停机时间来处理更新的对象。|  
  
## <a name="custom-storage-options"></a>自定义存储选项  
 您可以手动配置存储和主动缓存，而不是使用某个标准存储设置。 创建自定义存储设置之前，可能需要首先单击 **“标准设置”** 选项，然后将滑块移动到与要使用的配置最相匹配的标准设置。 然后，若要创建自定义配置，请单击 **“自定义设置”** 选项并单击 **“选项”**。  
  
-   可以指定数据源中的更改是否触发对缓存的更新。 若要允许可接受级别的偏差，可以指定更新数据源后的一个最小静默间隔。 还可以指定一个静默间隔覆盖，如果对数据源进行的更改之间的间隔从未达到最小值，则它将在指定期限之后更新缓存。  
  
-   可以指定在更新发生时是否删除过时缓存。 如果选择该选项，则当超过指定滞后时间时，服务器将在更新缓存时切换到实时关系 OLAP (ROLAP)。 如果不选择该选项，则服务器在生成新的多维 OLAP (MOLAP) 缓存时继续查询陈旧的多维 OLAP (MOLAP) 缓存。  
  
     可以指定在更改与删除过时缓存之间必须存在的滞后时间间隔。 这是在删除过时缓存之前用户可以继续浏览其中的数据的时间量。 如果发生更改且仍在该间隔结束时更新或处理缓存，则查询将被重定向到 ROLAP。  
  
-   如果要定期更新已缓存的 MOLAP 对象而不考虑对数据源所做的更改，则可以计划对缓存进行强制更新。 数据库的大小及由源数据更改频率分配的滞后时间不同，实时 OLAP 的好处也有所不同。 您希望用户尽可能频繁地向缓存（而不是向 ROLAP）发送查询。  
  
 如果选中 **“对维度应用设置”** 复选框，则同一存储设置还将应用到与该度量值组相关的维度。 维度值最初与分区值相同。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的分区](partitions-in-multidimensional-models.md)  
  
  
