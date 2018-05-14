---
title: IsDefaultImage 元素 (XML) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 115e65185a420594ebbd0aacca2f9d7be4175633
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="isdefaultimage-element-xml"></a>IsDefaultImage 元素 (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指示可以通过将此关系导航到其他表以及提取具有属性 IsDefaultImage 的成员，获取此实体的默认图像。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultImage>...</IsDefaultImage>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|false|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**RelationshipEndVisualizationProperties**元素， **IsDefaultImage**元素指示可以通过导航到其他实例的末尾来获取此实体的默认图像关系。 默认值**false**指示没有要从中获取的默认图像。  
  
  
