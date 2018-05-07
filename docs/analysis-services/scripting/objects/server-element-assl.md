---
title: 服务器元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 74c4b5a75dee0e7c9ff5428b6c7aa3c134e1c0b7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
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
  
  
