---
title: DbTableName 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- DbTableName
helpviewer_keywords:
- DbTableName element
ms.assetid: 842cae85-ab9c-4c75-ab44-51a4d9b1b943
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 491384b3b7f566faf733d27060ebc21e8a680bcd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153448"
---
# <a name="dbtablename-element-assl"></a>DbTableName 元素 (ASSL)
  包含父元素绑定到的表的名称。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TableBinding> <!-- or TableNotification -->  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableBinding>  
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
|父元素|[TableBinding](../data-type/binding-data-type-assl.md)， [TableNotification](../objects/tablenotification-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`DbTableName`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.TableBinding>和<xref:Microsoft.AnalysisServices.TableNotification>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
