---
title: CreatedTimestamp 元素 (ASSL) |Microsoft Docs
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
- CreatedTimestamp Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CreatedTimestamp
helpviewer_keywords:
- CreatedTimestamp element
ms.assetid: 35f5dd33-ea82-4be3-a117-69136aa9d1a4
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bab2bbc51422d6062b5f7df97fd3ff7b17e40c5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235617"
---
# <a name="createdtimestamp-element-assl"></a>CreatedTimestamp 元素 (ASSL)
  包含父元素的只读创建时间戳。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Assembly> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CreatedTimestamp>...</CreatedTimestamp>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|DateTime|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[程序集](../objects/assembly-element-assl.md)，[多维数据集](../objects/cube-element-assl.md)，[数据库](../objects/database-element-assl.md)， [DataSource](../objects/datasource-element-assl.md)， [DataSourceView](../objects/datasourceview-element-assl.md)，[维度](../objects/dimension-element-assl.md)， [MdxScript](../objects/mdxscript-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[分区](../objects/partition-element-assl.md)，[权限](../data-type/permission-data-type-assl.md)，[透视](../objects/perspective-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `CreatedTimestamp`元素包含一个只读`DateTime`值，该值表示的日期和时间的给定实例创建对象时[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 此元素的值不能为空。  
  
 父级对应的元素`CreatedTimestamp`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.Assembly>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataSource>， <xref:Microsoft.AnalysisServices.DataSourceView>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MdxScript>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>， <xref:Microsoft.AnalysisServices.Partition>， <xref:Microsoft.AnalysisServices.Permission>，并<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
