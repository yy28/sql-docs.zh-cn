---
title: "类型元素 (MiningStructureColumn) (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (MiningStructureColumn)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1fbc9ce30cd9f436a3bce1d96e532d6264b08a2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-miningstructurecolumn-assl"></a>Type 元素 (MiningStructureColumn) (ASSL)
  包含的一种[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*长*|64 位有符号整数。 此数据类型映射到**Int64**中数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 和是 DBTYPE_I8 数据类型在 OLE DB。|  
|*Boolean*|一个布尔值。 此数据类型映射到**布尔**.NET Framework 和 OLE DB 中的 DBTYPE_BOOL 数据类型中的数据类型。|  
|*Text*|Unicode 字符的以 Null 值结束的流。 此数据类型映射到**字符串**.NET Framework 和 OLE DB 中的 DBTYPE_WSTR 数据类型中的数据类型。|  
|*双*|双精度浮点数字的范围内-1.79 e + 308 到 1.79 e + 308。 此数据类型映射到**Double** .NET Framework 和 OLE DB 中的 DBTYPE_R8 数据类型中的数据类型。|  
|*日期*|双精度浮点数字的形式存储的日期数据。 整数部分是自 1899 年 12 月 30 日以来的天数，而小数部分是不足一天的部分。 此数据类型映射到**DateTime** .NET Framework 和 OLE DB 中的 DBTYPE_DATE 数据类型中的数据类型。|  
|*表*|嵌套表。 此数据类型映射到 OLE DB 中的 DBTYPE_HCHAPTER 数据类型。<br /><br /> 注意：.NET Framework 中的表列不具有等效的内部数据类型，但改为支持**DataReader**类。|  
  
 对应于的允许值为枚举**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>。  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

