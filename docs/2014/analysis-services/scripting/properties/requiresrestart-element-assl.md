---
title: RequiresRestart 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RequiresRestart Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RequiresRestart
helpviewer_keywords:
- RequiresRestart element
ms.assetid: 9e98f956-c41e-4e15-a7bd-e17c10ee6fc6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 752acb9d560ba62d74a3b5486c79279fb49fd2a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120877"
---
# <a name="requiresrestart-element-assl"></a>RequiresRestart 元素 (ASSL)
  包含只读的值与相关联[ServerProperty](../objects/serverproperty-element-assl.md)元素，用于确定是否更改服务器属性的值需要，重新启动实例才能使更改生效。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ServerProperty>  
   ...  
   <RequiresRestart>...</RequiresRestart>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ServerProperty](../objects/serverproperty-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`RequiresRestart`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>请参阅  
 [ServerProperties 元素&#40;ASSL&#41;](../collections/serverproperties-element-assl.md)   
 [服务器元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
