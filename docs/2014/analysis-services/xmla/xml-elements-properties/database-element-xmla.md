---
title: 数据库元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5861be2ad0f5975ef5b95c3f4b077a065b560e02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171957"
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
  标识包含父对象表示的维度的数据库[对象](object-element-dimension-xmla.md)元素。  
  
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
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[对象](object-element-dimension-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Database` 元素是包含 Analysis Services 数据库名称的对象标识符，该数据库包含由 `Object` 元素表示的维度。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集元素&#40;XMLA&#41;](cube-element-xmla.md)   
 [维度元素&#40;XMLA&#41;](dimension-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
