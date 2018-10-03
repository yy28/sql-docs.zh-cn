---
title: ColumnID 元素 (ColumnBinding) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ColumnID Element (ColumnBinding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: f4edf532-7e40-4ee2-9b5e-48b3c3de7a74
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c78d29225c8cec759ffda970e82866e1a7fe9b2f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184357"
---
# <a name="columnid-element-columnbinding-assl"></a>ColumnID 元素 (ColumnBinding) (ASSL)
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ColumnBinding](../data-type/binding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`ColumnID`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ColumnBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
