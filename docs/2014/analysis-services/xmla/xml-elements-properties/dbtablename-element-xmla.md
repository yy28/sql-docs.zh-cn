---
title: DbTableName 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DbTableName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DbTableName
- microsoft.xml.analysis.dbtablename
- urn:schemas-microsoft-com:xml-analysis#DbTableName
helpviewer_keywords:
- DbTableName element
ms.assetid: 0ffda645-2a88-4f42-8929-9d7385c19a74
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81caaee312e7c6978dbd66fec666aaa37b6efe3b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48056817"
---
# <a name="dbtablename-element-xmla"></a>DbTableName 元素 (XMLA)
  包含父级所使用的表的名称[TableNotification](tablenotification-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TableNotification>  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableNotification>  
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
|父元素|[TableNotification](tablenotification-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [DbSchemaName 元素&#40;XMLA&#41;](name-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
