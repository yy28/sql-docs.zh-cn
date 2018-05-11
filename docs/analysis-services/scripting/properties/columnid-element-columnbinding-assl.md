---
title: ColumnID 元素 (ColumnBinding) (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 59cf18b22220840489ba02bb155a7ab7b6f91d64
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="columnid-element-columnbinding-assl"></a>ColumnID 元素 (ColumnBinding) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含数据项绑定到的表中的列的标识符 (ID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ColumnBinding>  
   ...  
   <ColumnID>...</ColumnID>  
   ...  
</ColumnBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**ColumnID**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ColumnBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
