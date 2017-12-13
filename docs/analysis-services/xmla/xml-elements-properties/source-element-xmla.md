---
title: "源元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Source Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Source
- http://schemas.microsoft.com/analysisservices/2003/engine#Source
- microsoft.xml.analysis.source
helpviewer_keywords: Source element
ms.assetid: 4d4665ae-e20f-4baf-ab0f-848660caf500
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 03c4eddd80a362226be6989d00c56e4b4a53280c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="source-element-xmla"></a>Source 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]表示一个源分区合并期间[MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)命令。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[源](../../../analysis-services/xmla/xml-elements-properties/sources-element-xmla.md)|  
|子元素|[CubeID](../../../analysis-services/xmla/xml-elements-properties/cubeid-element-xmla.md)， [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)， [MeasureGroupID](../../../analysis-services/xmla/xml-elements-properties/measuregroupid-element-xmla.md)， [PartitionID](../../../analysis-services/xmla/xml-elements-properties/partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **源**元素是对要合并到指定目标分区的单个分区的对象引用**目标**元素的父**MergePartitions**元素。  
  
## <a name="example"></a>示例  
 下面的示例将 `Internet Sales` 度量值组的全部四个分区合并到了 `Internet_Sales_2004` 目标分区中。 此示例指**Adventure Works**多维数据集的[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]示例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [目标元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
