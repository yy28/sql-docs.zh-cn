---
title: PerspectiveMeasureGroup 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PerspectiveMeasureGroup Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveMeasureGroup
helpviewer_keywords:
- PerspectiveMeasureGroup data type
ms.assetid: 5927120d-f30e-4f87-8523-6d17012817d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b11d6f419d3cfa9f65eca1442198fad39cd526f4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224767"
---
# <a name="perspectivemeasuregroup-data-type-assl"></a>PerspectiveMeasureGroup 数据类型 (ASSL)
  定义一个基元数据类型，表示有关度量值组中的信息[角度来看](../objects/perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PerspectiveMeasureGroup>  
   <MeasureGroupID>...</MeasureGroupID>  
   <Measures>...</Measures>  
   <Annotations>...</Annotations>  
</PerspectiveMeasureGroup>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[批注](../collections/annotations-element-assl.md)， [MeasureGroupID](../properties/id-element-assl.md)，[度量值](../collections/measures-element-assl.md)|  
|派生元素|[MeasureGroup](../objects/group-element-assl.md) ([MeasureGroups](../collections/groups-element-assl.md)的集合[角度来看](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>备注  
 透视中的度量值组的结构与基础多维数据集中的度量值组的相同。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
