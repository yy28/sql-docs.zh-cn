---
title: CreatedTimestamp 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14c1f03f7279ebdd1c5ef96cb1474a9baa7f89e7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="createdtimestamp-element-assl"></a>CreatedTimestamp 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|DateTime|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)，[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)，[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)，[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)，[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **CreatedTimestamp**元素包含一个只读的**DateTime**值，该值表示的日期和时间的给定实例创建对象时[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. 此元素的值不能为空。  
  
 对应的父级的元素**CreatedTimestamp**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Assembly>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.Database>， <xref:Microsoft.AnalysisServices.DataSource>， <xref:Microsoft.AnalysisServices.DataSourceView>， <xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.MdxScript>， <xref:Microsoft.AnalysisServices.MeasureGroup>， <xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningStructure>， <xref:Microsoft.AnalysisServices.Partition>， <xref:Microsoft.AnalysisServices.Permission>，和<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
