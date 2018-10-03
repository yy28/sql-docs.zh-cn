---
title: DataSourceViewID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourceViewID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataSourceViewID
helpviewer_keywords:
- DataSourceViewID element
ms.assetid: dcf617fe-0bf6-4767-af35-07c0c7fd96e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bea1a67eaedc1119ad5260df435266649d11f048
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225197"
---
# <a name="datasourceviewid-element-assl"></a>DataSourceViewID 元素 (ASSL)
  标识[DataSourceView](../objects/datasourceview-element-assl.md)元素与关联[绑定](../data-type/binding-data-type-assl.md)父元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSourceViewBinding> <!-- or DSVTableBinding -->  
   ...  
   <DataSourceViewID>...</DataSourceViewID>  
   ...  
</DataSourceViewBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md)， [DSVTableBinding](../data-type/tablebinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`DataSourceViewID`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.DataSourceViewBinding>和<xref:Microsoft.AnalysisServices.DSVTableBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
