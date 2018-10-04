---
title: AxesInfo 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AxesInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#AxesInfo
- microsoft.xml.analysis.axesinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#AxesInfo
helpviewer_keywords:
- AxesInfo element
ms.assetid: 15cfa67d-5acd-4737-8a81-2df34b334d3f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7bde7feb88ad570665200c1c3357bbba4127a963
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178487"
---
# <a name="axesinfo-element-xmla"></a>AxesInfo 元素 (XMLA)
  包含一系列[AxisInfo](axisinfo-element-xmla.md)元素，表示轴的元数据包含在父[OlapInfo](olapinfo-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<OlapInfo>  
   ...  
   <AxesInfo>  
      <AxisInfo>...</AxisInfo>  
   </AxesInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[OlapInfo](olapinfo-element-xmla.md)|  
|子元素|[AxisInfo](axisinfo-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 `AxesInfo` 元素为由使用 `AxisInfo` 数据类型的 `root` 元素返回的多维数据集中的每个轴包含一个 `MDDataSet` 元素。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
