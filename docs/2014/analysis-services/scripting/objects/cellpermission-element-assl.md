---
title: CellPermission 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellPermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CellPermission
helpviewer_keywords:
- CellPermission element
ms.assetid: 54a6afc0-1fcb-4b24-851a-6d81e1fe0efc
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f763ee90f4812ef86cae0cd24e96e5fb02b05087
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293367"
---
# <a name="cellpermission-element-assl"></a>CellPermission 元素 (ASSL)
  描述的权限的成员[角色](role-element-assl.md)元素内的各个单元上享有[多维数据集](cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CellPermissions>  
   <CellPermission>  
      <Access>...</Access>  
            <Description>...</Description>  
      <Expression>...</Expression>  
      <Annotations>...</Annotations>  
   </CellPermission>  
</CellPermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CellPermissions](../collections/cellpermissions-element-assl.md)|  
|子元素|[访问](../properties/access-element-assl.md)，[批注](../collections/annotations-element-assl.md)，[说明](../properties/description-element-assl.md)，[表达式](../properties/expression-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CellPermission>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
