---
title: 服务器元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9715dd8e6ebd5c080362004850674adc3113c8c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="server-element-assl"></a>Server 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述的实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Server>  
   <!—These elements are common to each major object -->  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Annotations>...</Annotations>  
   <!-- server elements or properties -->  
   <ProductName>...</ProductName>  
   <Edition>...</Edition>  
   <EditionId>...</Edition>  
   <Version>...</Version>  
   <ServerMode>...</ServerMode>  
   <ProductLevel>...</Databases>  
   <Databases>...</Databases>  
   <Assemblies>...</Assemblies>  
   <Traces>...</Traces>  
   <Roles>...</Roles>  
   <ServerProperties>...</ServerProperties>  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [ProductName](../../../analysis-services/scripting/properties/productname-element-assl.md)，[版本](../../../analysis-services/scripting/properties/edition-element-assl.md)， [EditionId](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md)，[版本](../../../analysis-services/scripting/properties/version-element-assl.md)， [ServerMode](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md)， [ProductLevel](../../../analysis-services/xmla/xml-elements-properties/productlabel-element.md)，[数据库](../../../analysis-services/scripting/collections/databases-element-assl.md)，[程序集](../../../analysis-services/scripting/collections/assemblies-element-assl.md)，[跟踪](../../../analysis-services/scripting/collections/traces-element-assl.md)，[角色](../../../analysis-services/scripting/collections/roles-element-assl.md)，[ServerProperties](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>注释  
 **服务器**元素表示的实例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，并作为 Analysis Services 脚本语言 (ASSL) 节点层次结构中最顶层节点。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
