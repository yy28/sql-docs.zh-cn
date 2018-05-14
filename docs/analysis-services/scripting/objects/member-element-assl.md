---
title: 成员元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a266e1c3524a489f1f75cf6675dc8a9b4677d9a9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="member-element-assl"></a>Member 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的一个成员的名称[组](../../../analysis-services/scripting/objects/group-element-assl.md)元素或[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Members>  
   <Member>  
      <Name>...</Name>  
   </Member>  
</Members>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[成员](../../../analysis-services/scripting/collections/members-element-assl.md)|  
|子元素|[名称](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**成员**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Group>和<xref:Microsoft.AnalysisServices.Role>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
