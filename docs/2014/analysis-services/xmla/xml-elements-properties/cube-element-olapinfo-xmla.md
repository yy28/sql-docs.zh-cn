---
title: 多维数据集元素 (OlapInfo) (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Cube Element (OlapInfo)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords:
- Cube element
ms.assetid: c2b6fe41-6ad4-4181-98a9-3a2517f0b7cc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a85f4c0eaf73ac3e971894fbfc4e42eb6c6a5045
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111217"
---
# <a name="cube-element-olapinfo-xmla"></a>Cube 元素 (OlapInfo) (XMLA)
  包含父多维数据集有关的信息[CubeInfo](cubeinfo-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeInfo>  
   <Cube>  
      <CubeName>...</CubeName>  
      <LastDataUpdate>...</LastDataUpdate>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
   </Cube>  
   ...  
</CubeInfo>  
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
|父元素|[CubeInfo](cubeinfo-element-xmla.md)|  
|子元素|[多维数据集名称](name-element-xmla.md)， [LastDataUpdate](../xml-elements-commands/update-element-xmla.md)， [LastSchemaUpdate](lastschemaupdate-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
