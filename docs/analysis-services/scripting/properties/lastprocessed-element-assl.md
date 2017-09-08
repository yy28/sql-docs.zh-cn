---
title: "LastProcessed 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- LastProcessed Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- LastProcessed
helpviewer_keywords:
- LastProcessed element
ms.assetid: df3d1f6f-705c-4408-9eb3-c550a1dec450
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2b75c11f304c72eec83f6eb5baa429ad33a3c0f8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lastprocessed-element-assl"></a>LastProcessed 元素 (ASSL)
  包含只读时间戳，该时间戳指示上次处理包含父元素的数据库的时间。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
      <LastProcessed>...</LastProcessed>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|DateTime|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]维护的值**LastProcessed**元素。 该值仅在处理包含父元素的数据库时才更改。 单独处理的父元素不会更改的值**LastProcessed**元素。  
  
 对应的父级的元素**LastProcessed**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
