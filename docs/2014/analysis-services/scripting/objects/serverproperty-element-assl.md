---
title: ServerProperty 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d84d9fc4bb78969265399d2a67207ea15e753f39
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185767"
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ServerProperties](../collections/serverproperties-element-assl.md)|  
|子元素|[DefaultValue](../properties/value-element-assl.md)， [DisplayFlag](../properties/displayflag-element-assl.md)，[名称](../properties/name-element-assl.md)， [PendingValue](../properties/pendingvalue-element-assl.md)， [RequiresRestart](../properties/requiresrestart-element-assl.md)，[值](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 `ServerProperty`元素描述的数据和元数据与实例关联的服务器属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 与 Analysis Services 脚本语言 (ASSL) 中的其他集合包含的元素不同，`ServerProperty` 元素使用名称/值对（而不是显式命名的元素）来描述服务器属性。 名称/值对可提供灵活性和可扩展性。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>请参阅  
 [服务器元素&#40;ASSL&#41;](server-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
