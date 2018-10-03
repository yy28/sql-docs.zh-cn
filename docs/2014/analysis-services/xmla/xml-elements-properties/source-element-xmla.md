---
title: Source 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Source Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Source
- http://schemas.microsoft.com/analysisservices/2003/engine#Source
- microsoft.xml.analysis.source
helpviewer_keywords:
- Source element
ms.assetid: 4d4665ae-e20f-4baf-ab0f-848660caf500
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06c69de2879b2298b180b6dd487fe2dc28f09684
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095717"
---
# <a name="source-element-xmla"></a>Source 元素 (XMLA)
  表示一个源分区期间合并[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Sources>  
   <Source>  
      <DatabaseID>...</DatabaseID>  
      <CubeID>...</CubeID>  
      <MeasureGroupID>...</MeasureGroupID>  
      <PartitionID>...</PartitionID>  
   </Source>  
</Sources>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[源](sources-element-xmla.md)|  
|子元素|[CubeID](id-element-xmla.md)， [DatabaseID](databaseid-element-xmla.md)， [MeasureGroupID](measuregroupid-element-xmla.md)， [PartitionID](partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `Source` 元素是对单个分区的对象引用，该单个分区为要合并到父级 `Target` 元素的 `MergePartitions` 元素所指定的目标分区的单个分区。  
  
## <a name="example"></a>示例  
 下面的示例将 `Internet Sales` 度量值组的全部四个分区合并到了 `Internet_Sales_2004` 目标分区中。 此示例引用**Adventure Works**多维数据集[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]示例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
     <Source>        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>        <CubeID>Adventure Works</CubeID>        <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>        <PartitionID>Internet_Sales_2001</PartitionID>     </Source>     <Source>        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>        <CubeID>Adventure Works</CubeID>      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>      <PartitionID>Internet_Sales_2002</PartitionID>    </Source>    <Source>      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>      <PartitionID>Internet_Sales_2003</PartitionID>    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>请参阅  
 [Target 元素&#40;XMLA&#41;](../xml-elements-properties/target-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
