---
title: "ServerProperty 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ServerProperty Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- SERVERPROPERTY
helpviewer_keywords:
- ServerProperty element
ms.assetid: f152a1b5-0972-40d8-907f-f131c2a108bb
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4352648eb41332b57e3d95508a6985982b4509e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="serverproperty-element-assl"></a>ServerProperty 元素 (ASSL)
  定义与关联的服务器属性[服务器](../../../analysis-services/scripting/objects/server-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ServerProperties](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)|  
|子元素|[DefaultValue](../../../analysis-services/scripting/properties/defaultvalue-element-assl.md)， [DisplayFlag](../../../analysis-services/scripting/properties/displayflag-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [PendingValue](../../../analysis-services/scripting/properties/pendingvalue-element-assl.md)， [RequiresRestart](../../../analysis-services/scripting/properties/requiresrestart-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 **ServerProperty**元素描述的数据和元数据与实例关联的服务器属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 与在 Analysis Services 脚本语言 (ASSL)，其他集合中包含元素不同**ServerProperty**元素而不是显式命名的元素使用名称/值对描述服务器属性。 名称/值对可提供灵活性和可扩展性。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另请参阅  
 [服务器元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

