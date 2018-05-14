---
title: 数据库元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f874d72700646456fa046b820f0fdf29e4738d58
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  标识包含由父维度的数据库[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Object>  
   ...  
   <Database>...</Database>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **数据库**元素是包含包含由该维度的 Analysis Services 数据库的名称的对象标识符**对象**元素。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md)   
 [维度元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
