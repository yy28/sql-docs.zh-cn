---
title: DataType 元素 (ASSL) |Microsoft Docs
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
- DataType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataType
helpviewer_keywords:
- DataType element
ms.assetid: efe6f717-8288-4ca2-85ed-9b63d27c02d8
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16bc234f74aa8d6eb80607c7d03d63da8130e8ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231867"
---
# <a name="datatype-element-assl"></a>DataType 元素 (ASSL)
  定义关联元素的数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem> <!-- or Measure -->  
   ...  
   <DataType>...</DataType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)，[度量值](../objects/measure-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DataType` 的值是在 `System.Data.OleDb.OleDbType` 枚举中定义的。 但是，只有下表中的枚举值在 `DataType` 元素中有效。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*BigInt*|64 位有符号整数。 此数据类型映射到`Int64`中的数据类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 和 DBTYPE_I8 数据类型在 OLE DB 中。|  
|*bool*|一个布尔值。 此数据类型映射到 .NET Framework 中的 `Boolean` 数据类型和 OLE DB 中的 DBTYPE_BOOL 数据类型。|  
|*货币*|货币值，范围从-2<sup>63</sup> （或-922337203685，477.5808） 到 2<sup>63</sup>-1 （或 + 922337203685，477.5807），精度为千分之十个货币单位。 此数据类型映射到 .NET Framework 中的 `Decimal` 数据类型和 OLE DB 中的 DBTYPE_CY 数据类型。|  
|*日期*|日期数据，存储为双精度浮点数字。 整数部分是自 1899 年 12 月 30 日以来的天数，而小数部分是不足一天的部分。 此数据类型映射到 .NET Framework 中的 `DateTime` 数据类型和 OLE DB 中的 DBTYPE_DATE 数据类型。|  
|*双精度*|双精度浮点数范围在-1.79E + 308 到 1.79E + 308 之间。 此数据类型映射到 .NET Framework 中的 `Double` 数据类型和 OLE DB 中的 DBTYPE_R8 数据类型。|  
|*Integer*|32 位有符号整数。 此数据类型映射到 .NET Framework 中的 `Int32` 数据类型和 OLE DB 中的 DBTYPE_I4 数据类型。|  
|*Single*|单精度浮点数范围在-3.40E + 38 到 3.40E + 38 之间。 此数据类型映射到 .NET Framework 中的 `Single` 数据类型和 OLE DB 中的 DBTYPE_R4 数据类型。|  
|*SmallInt*|16 位有符号整数。 此数据类型映射到 .NET Framework 中的 `Int16` 数据类型和 OLE DB 中的 DBTYPE_I2 数据类型。|  
|*TinyInt*|一个 8 位有符号整数。 此数据类型映射到 .NET Framework 中的 `SByte` 数据类型和 OLE DB 中的 DBTYPE_I1 数据类型。|  
|*UnsignedBigInt*|一个 64 位无符号整数。 此数据类型映射到 .NET Framework 中的 `UInt64` 数据类型和 OLE DB 中的 DBTYPE_UI8 数据类型。|  
|*UnsignedInt*|32 位无符号整数。 此数据类型映射到 .NET Framework 中的 `UInt32` 数据类型和 OLE DB 中的 DBTYPE_UI4 数据类型。|  
|*UnsignedSmallInt*|16 位无符号整数。 此数据类型映射到 .NET Framework 中的 `UInt16` 数据类型和 OLE DB 中的 DBTYPE_UI2 数据类型。|  
|*WChar*|Unicode 字符的以 Null 值结束的流。 此数据类型映射到 .NET Framework 中的 `String` 数据类型和 OLE DB 中的 DBTYPE_WSTR 数据类型。|  
|*继承*|数据类型`DataItem`中包含[源](source-element-measure-assl.md)元素的`Measure`元素。 **注意：** 适用于`Measure`元素。|  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
