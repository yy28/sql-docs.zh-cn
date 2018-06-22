---
title: MaxActiveConnections 元素 (ASSL) |Microsoft 文档
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
- MaxActiveConnections Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MaxActiveConnections element
ms.assetid: 0dc5b64d-061d-409f-95c0-4c63f87f5ee4
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: df2dafc69a97d1beb954100413761c07878881d4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016682"
---
# <a name="maxactiveconnections-element-assl"></a>MaxActiveConnections 元素 (ASSL)
  包含的最大允许的元素派生自的并发连接数[数据源](../data-type/datasource-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <MaxActiveConnections>...</MaxActiveConnections>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|`10`|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSource](../data-type/datasource-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 如果此元素的值设置为零，则最大并发连接数取决于用来访问数据源的数据插件。 如果此元素的值设置为负值，则对最大并发连接数没有限制。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  