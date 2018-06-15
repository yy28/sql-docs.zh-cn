---
title: 类型元素 (MiningStructureColumn) (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bcb7cec0d968e1320bdafc4bf53d25d6efdabc6f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040409"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Type 元素 (MiningStructureColumn) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*Long*|64 位有符号整数。 此数据类型映射到**Int64**中数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 和是 DBTYPE_I8 数据类型在 OLE DB。|  
|*Boolean*|一个布尔值。 此数据类型映射到**布尔**.NET Framework 和 OLE DB 中的 DBTYPE_BOOL 数据类型中的数据类型。|  
|*文本*|Unicode 字符的以 Null 值结束的流。 此数据类型映射到**字符串**.NET Framework 和 OLE DB 中的 DBTYPE_WSTR 数据类型中的数据类型。|  
|*双精度*|双精度浮点数字的范围内-1.79 e + 308 到 1.79 e + 308。 此数据类型映射到**Double** .NET Framework 和 OLE DB 中的 DBTYPE_R8 数据类型中的数据类型。|  
|*日期*|双精度浮点数字的形式存储的日期数据。 整数部分是自 1899 年 12 月 30 日以来的天数，而小数部分是不足一天的部分。 此数据类型映射到**DateTime** .NET Framework 和 OLE DB 中的 DBTYPE_DATE 数据类型中的数据类型。|  
|*表*|嵌套表。 此数据类型映射到 OLE DB 中的 DBTYPE_HCHAPTER 数据类型。<br /><br /> 注意：.NET Framework 中的表列不具有等效的内部数据类型，但改为支持**DataReader**类。|  
  
 对应于的允许值为枚举**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>。  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
