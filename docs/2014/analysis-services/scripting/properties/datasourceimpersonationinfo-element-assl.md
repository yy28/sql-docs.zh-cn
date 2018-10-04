---
title: DataSourceImpersonationInfo 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSourceImpersonationInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSourceImpersonationInfo element
ms.assetid: a153044b-2d6c-406b-aeb3-15bf096931f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed6feef09732e92b018cf73103ea2334888d86c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055151"
---
# <a name="datasourceimpersonationinfo-element-assl"></a>DataSourceImpersonationInfo 元素 (ASSL)
  包含用来连接到数据源时确定模拟行为的信息[数据库](../objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database>  
   <DataSourceImpersonationInfo>  
      <!-- Child elements are only those inherited from ImpersonationInfo -->  
   </DataSourceImpersonationInfo>  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[ImpersonationInfo 数据类型&#40;ASSL&#41;](../data-type/impersonationinfo-data-type-assl.md)|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[“数据库”](../objects/database-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
