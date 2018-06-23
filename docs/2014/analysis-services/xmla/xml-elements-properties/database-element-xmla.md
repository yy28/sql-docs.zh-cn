---
title: 数据库元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.database
- http://schemas.microsoft.com/analysisservices/2003/engine#Database
- urn:schemas-microsoft-com:xml-analysis#Database
helpviewer_keywords:
- Database element
ms.assetid: 2ded06c4-4eaf-4ccb-a416-41ee51ced8bc
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f1b643a12ab1dbf2dc151fe91a8663b138e581ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014393"
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
  标识包含由父维度的数据库[对象](object-element-dimension-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Object>  
   ...  
   <Database>...</Database>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[对象](object-element-dimension-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Database` 元素是包含 Analysis Services 数据库名称的对象标识符，该数据库包含由 `Object` 元素表示的维度。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;XMLA&#41;](cube-element-xmla.md)   
 [维度元素&#40;XMLA&#41;](dimension-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  