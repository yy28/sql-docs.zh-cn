---
title: "根元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Root Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Root
helpviewer_keywords: Root element
ms.assetid: ad3319d5-c3f0-49e3-b9c0-2fb77945c512
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 69ccda5c0189a9bc868ddb0220d7121f3f5fd8bf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="root-element-assl"></a>Root 元素 (ASSL)
  包含数据源的数据（行集）。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PushedDataSource>  
   ...  
   <Root>...</Root>  
   ...  
</PushedDataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|行集|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|  
|子元素|无|  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
