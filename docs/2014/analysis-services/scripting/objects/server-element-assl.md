---
title: 服务器元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39c4d780ade53dcb16d446237aa467f131614176
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106707"
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
|数据类型和长度|None|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[名称](../properties/name-element-assl.md)， [ID](../properties/id-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[说明](../properties/description-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [ProductName](../properties/productname-element-assl.md)， [Edition](../properties/edition-element-assl.md)， [EditionId](../../xmla/xml-elements-properties/editionid-element.md)，[版本](../properties/version-element-assl.md)， [ServerMode](../../xmla/xml-elements-properties/editionid-element.md)， [ProductLevel](../../xmla/xml-elements-properties/productlabel-element.md)，[数据库](../collections/databases-element-assl.md)，[程序集](../collections/assemblies-element-assl.md)，[跟踪](../collections/traces-element-assl.md)，[角色](../collections/roles-element-assl.md)，[ServerProperties](../collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>备注  
 `Server` 元素表示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例，并作为 Analysis Services 脚本语言 (ASSL) 节点层次结构的最顶层节点。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
