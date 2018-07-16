---
title: 常规 （存储选项对话框) (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c238f74f5041c0b2a549979bac0a9871847eca5e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306547"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>常规（“存储选项”对话框）（Analysis Services - 多维数据）
  可以使用 **中的** “存储选项” **对话框上的** “常规” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 选项卡，设置维度、多维数据集、度量值组或分区的存储模式和主动缓存设置。  
  
> [!NOTE]  
>  您必须熟悉存储模式和主动缓存功能，才可以修改这些设置。 有关详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**存储模式**|选择对象要使用的存储模式。<br /><br /> **MOLAP**<br /> 对象使用多维 OLAP (MOLAP) 存储。<br /><br /> **HOLAP**<br /> 对象使用混合 OLAP (HOLAP) 存储。<br /><br /> **ROLAP**<br /> 对象使用关系 OLAP (ROLAP) 存储。|  
|**启用了主动缓存**|启用主动缓存。<br /><br /> 注意：如果未选择此选项，则将禁用除“存储模式”  外的所有选项。|  
|**当数据更改时更新缓存**|使用在 **“通知”** 选项卡中选择的通知方法，可以在收到通知时更新对象的 MOLAP 映像。 有关“通知”选项卡的详细信息，请参阅[通知（“存储选项”对话框）（Analysis Services - 多维数据）](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)。<br /><br /> 注意：除非选择“启用主动缓存”  ，否则将禁用此选项。|  
|**指定静默间隔时间**|设置在主动缓存开始为对象创建新的 MOLAP 映像之前，对象处于无任何活动状态的最小时间间隔和时间单位。<br /><br /> 注意：除非选择“当数据更改时更新缓存”  ，否则将禁用此选项。|  
|**静默覆盖间隔**|设置在收到对象的通知之后，不管当前对象的活动状态如何，主动缓存开始为对象创建新的 MOLAP 映像之前的最大时间间隔和时间单位。 在达到此间隔后接收的通知不会取消此间隔所触发的 MOLAP 映像进程。<br /><br /> 注意：除非选择“当数据更改时更新缓存”  ，否则将禁用此选项。 另请注意，如果，不应设置此选项**存储模式**设置为**HOLAP**。|  
|**放弃过时的缓存**|指定开始创建新的 MOLAP 缓存和删除现有 MOLAP 缓存之间间隔的时间段。<br /><br /> 注意：除非选择“启用主动缓存”  ，否则将禁用此选项。 另请注意，如果，不应设置此选项**存储模式**设置为 HOLAP。|  
|**滞后时间**|为开始创建新的 MOLAP 缓存和删除现有 MOLAP 缓存之间间隔的时间段选择时间间隔和时间单位。<br /><br /> 注意：除非选择“放弃过时缓存”  ，否则将禁用此选项。 另请注意，如果，不应设置此选项**存储模式**设置为**HOLAP**。|  
|**定期更新缓存**|不管是否收到通知，都将定期更新 MOLAP 映像。<br /><br /> 注意：除非选择“启用主动缓存”  ，否则将禁用此选项。 另请注意，如果，不应设置此选项**存储模式**设置为**HOLAP**。|  
|**重新生成间隔时间**|选择在创建新的 MOLAP 映像之后，不管是否收到通知， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 再次为对象启动 MOLAP 映像进程之前的时间间隔和时间单位。 在达到此间隔后接收的通知不会取消此间隔所触发的 MOLAP 映像进程。<br /><br /> 注意：除非选择“定期更新缓存”  ，否则将禁用此选项。 另请注意，如果，不应设置此选项**存储模式**设置为**HOLAP**。|  
|**立即联机**|使对象立即联机。 如果设置此选项，则在重新生成 MOLAP 缓存时，对象将使用基础 ROLAP 存储区来解析查询。 如果未设置此选项，则只有在完成对象的 MOLAP 缓存之后，对象才会联机。|  
|**启用 ROLAP 聚合**|使用基础数据源的具体化视图来存储聚合。<br /><br /> 注意：如果基础数据源不支持具体化视图，则会在处理对象时发生错误。|  
|**对维度应用设置**|将存储模式和主动缓存设置应用于所关联的维度。|  
  
## <a name="see-also"></a>请参阅  
 [存储选项对话框的&#40;Analysis Services-多维数据&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [通知&#40;存储选项对话框&#41; &#40;Analysis Services-多维数据&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  
