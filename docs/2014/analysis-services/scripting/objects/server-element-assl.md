---
title: 服务器元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Server Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- server
helpviewer_keywords:
- Server element
ms.assetid: 92ca67f6-817e-4a75-9244-8f8bcf412190
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f2bcf6e40530a67f8c1e9c846ba88f6d77648a09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123910"
---
# <a name="server-element-assl"></a>Server 元素 (ASSL)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[Name](../properties/name-element-assl.md), [ID](../properties/id-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [Description](../properties/description-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [ProductName](../properties/productname-element-assl.md), [Edition](../properties/edition-element-assl.md), [EditionId](../../xmla/xml-elements-properties/editionid-element.md), [Version](../properties/version-element-assl.md), [ServerMode](../../xmla/xml-elements-properties/editionid-element.md), [ProductLevel](../../xmla/xml-elements-properties/productlabel-element.md), [Databases](../collections/databases-element-assl.md), [Assemblies](../collections/assemblies-element-assl.md), [Traces](../collections/traces-element-assl.md), [Roles](../collections/roles-element-assl.md), [ServerProperties](../collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>Remarks  
 `Server` 元素表示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例，并作为 Analysis Services 脚本语言 (ASSL) 节点层次结构的最顶层节点。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  