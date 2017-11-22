---
title: "多重性元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
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
applies_to: SQL Server 2016 Preview
ms.assetid: 441e3829-9009-4b32-a8c6-fa580663387f
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2483225abebeb66fe691ee11e33f1322a3f10dc0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="multiplicity-element-assl"></a>Multiplicity 元素 (ASSL)
  指示 RelationshipEnd 中的属性是位于关系的“一”方还是关系的“多”方。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEnd>  
   ...  
   <Multiplicity>...</Multiplicity>  
   ...  
</RelationshipEnd>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值||  
|基数|1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*其中一个*|这是主键方。|  
|*许多*|这是外键方。|  
  
 对应于的允许值为枚举**角色**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Multiplicity>。  
  
  
