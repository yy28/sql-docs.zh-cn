---
title: 源元素 (XMLA) |Microsoft 文档
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
- Sources Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.sources
- http://schemas.microsoft.com/analysisservices/2003/engine#Sources
- urn:schemas-microsoft-com:xml-analysis#Sources
helpviewer_keywords:
- Sources element
ms.assetid: fefe8f01-4c62-4b70-9bf6-f11d2f01623a
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f634df53b1eb92979caa699b25824d9345e00c21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128185"
---
# <a name="sources-element-xmla"></a>Sources 元素 (XMLA)
  包含一套[源](source-element-xmla.md)父元素[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MergePartitions>  
...  
   <Sources>  
      <Source>...</Source>  
   </Sources>  
...  
</MergePartitions>  
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
|父元素|[撰写 MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)|  
|子元素|[数据源](source-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="example"></a>示例  
 下面的示例将 `Internet Sales` 度量值组的全部四个分区合并到了 `Internet_Sales_2004` 目标分区中。 此示例使用了 [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] 示例 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库的 Adventure Works DW 多维数据集。  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>database</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  