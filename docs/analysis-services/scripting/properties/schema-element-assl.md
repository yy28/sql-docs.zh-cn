---
title: 架构元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9822bbf6112673c5e03c382063af2ed017b8d5ca
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="schema-element-assl"></a>Schema 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含数据源视图的架构。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|架构|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **架构**使用中的数据集的 XML 架构定义 (XSD) 语言格式表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 中，使用适用于数据集和其他特定于这种用法中的数据定义一些扩展语言 (DDL)。 DataSet 可定义从 XSD 到关系架构的灵活映射，然后以更为规范化的格式返回 XSD。 只有此规范化的格式在数据源中才有效。  
  
 对应于的父元素**架构**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DataSourceView>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
