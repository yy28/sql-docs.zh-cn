---
title: ServerProperty 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ServerProperty Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SERVERPROPERTY
helpviewer_keywords:
- ServerProperty element
ms.assetid: f152a1b5-0972-40d8-907f-f131c2a108bb
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c6af3d46fac2b6ed02ff4cd261a8f5361d466ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300927"
---
# <a name="serverproperty-element-assl"></a>ServerProperty 元素 (ASSL)
  定义与关联的服务器属性[Server](server-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ServerProperties>  
   <ServerProperty>  
      <Name>...</Name>  
      <Value>...</Value>  
            <RequiresRestart>...</RequiresRestart>  
            <PendingValue>...</PendingValue>  
      <DefaultValue>...</DefaultValue>  
      <DisplayFlag>...</DisplayFlag>  
   </ServerProperty>  
</ServerProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ServerProperties](../collections/serverproperties-element-assl.md)|  
|子元素|[DefaultValue](../properties/value-element-assl.md)， [DisplayFlag](../properties/displayflag-element-assl.md)，[名称](../properties/name-element-assl.md)， [PendingValue](../properties/pendingvalue-element-assl.md)， [RequiresRestart](../properties/requiresrestart-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 `ServerProperty`元素描述的数据和元数据与实例关联的服务器属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 与 Analysis Services 脚本语言 (ASSL) 中的其他集合包含的元素不同，`ServerProperty` 元素使用名称/值对（而不是显式命名的元素）来描述服务器属性。 名称/值对可提供灵活性和可扩展性。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>请参阅  
 [服务器元素&#40;ASSL&#41;](server-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
