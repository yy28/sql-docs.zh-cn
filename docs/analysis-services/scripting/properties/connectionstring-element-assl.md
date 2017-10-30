---
title: "ConnectionString 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ConnectionString Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: f74181c4-7df7-4fbd-94dd-e4ad03dffe14
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dc85faaf914bbcec9b7ff810fa950a74a146bb97
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="connectionstring-element-assl"></a>ConnectionString 元素 (ASSL)
  包含的加密的连接字符串[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**ConnectionString**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

