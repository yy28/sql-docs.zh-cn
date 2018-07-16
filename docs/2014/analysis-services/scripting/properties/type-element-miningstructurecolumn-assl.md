---
title: Type 元素 (MiningStructureColumn) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (MiningStructureColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ce9327fb28e9f452e643ded604f2a8dd72a084
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304237"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Type 元素 (MiningStructureColumn) (ASSL)
  包含的类型[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Long*|64 位有符号整数。 此数据类型映射到`Int64`中的数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 和 DBTYPE_I8 数据类型在 OLE DB 中。|  
|*Boolean*|一个布尔值。 此数据类型映射到 .NET Framework 中的 `Boolean` 数据类型和 OLE DB 中的 DBTYPE_BOOL 数据类型。|  
|*Text*|Unicode 字符的以 Null 值结束的流。 此数据类型映射到 .NET Framework 中的 `String` 数据类型和 OLE DB 中的 DBTYPE_WSTR 数据类型。|  
|*双精度*|双精度浮点数的范围内-1.79E + 308 到 1.79E + 308 之间。 此数据类型映射到 .NET Framework 中的 `Double` 数据类型和 OLE DB 中的 DBTYPE_R8 数据类型。|  
|*日期*|日期数据，存储为双精度浮点数字。 整数部分是自 1899 年 12 月 30 日以来的天数，而小数部分是不足一天的部分。 此数据类型映射到 .NET Framework 中的 `DateTime` 数据类型和 OLE DB 中的 DBTYPE_DATE 数据类型。|  
|*表*|嵌套表。 此数据类型映射到 OLE DB 中的 DBTYPE_HCHAPTER 数据类型。 **注意：** .NET Framework 中的表列没有等效的内部数据类型，但受`DataReader`类。|  
  
 与允许的值相对应的枚举`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>。  
  
 父级对应的元素`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.MiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
