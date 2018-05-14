---
title: 值元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9acc8856dfaaa250d1addc8bd1df72325a5d86c7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="value-element-assl"></a>Value 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含父元素的值。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AlgorithmParameter> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Value>...</Value>  
   ...  
</AlgorithmParameter>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|请参阅下表。|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
|祖先或父级|数据类型|  
|------------------------|---------------|  
|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|任何 simpleType|  
|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|任何 simpleType|  
|其他|字符串|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)，[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)， [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)， [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)， [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **值**元素包含与父对象关联的值。 所需的值**值**元素异的父元素下表中所述。  
  
|父元素|预期值|  
|--------------------|--------------------|  
|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|算法参数的值。|  
|[批注](../../../analysis-services/scripting/objects/annotation-element-assl.md)|批注的值。|  
|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|用于计算关键绩效指标 (KPI) 的值的多维表达式 (MDX) 表达式。|  
|[ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)|报表格式参数的值。|  
|[ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)|用于计算报表参数值的 MDX 表达式。|  
|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|当前运行的实例的服务器属性值。|  
  
 对应的父级的元素**值**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AlgorithmParameter>， <xref:Microsoft.AnalysisServices.Annotation>， <xref:Microsoft.AnalysisServices.Kpi>， <xref:Microsoft.AnalysisServices.ReportParameter>，和<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
