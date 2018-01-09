---
title: "DbTableName 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DbTableName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DbTableName
helpviewer_keywords: DbTableName element
ms.assetid: 842cae85-ab9c-4c75-ab44-51a4d9b1b943
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e7ab467cf2b2d9445789389ff41b9df726c1c8c4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="dbtablename-element-assl"></a>DbTableName 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含父元素绑定到的表的名称。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TableBinding> <!-- or TableNotification -->  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)， [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应的父级的元素**DbTableName**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.TableBinding>和<xref:Microsoft.AnalysisServices.TableNotification>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
