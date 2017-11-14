---
title: "FieldAttributeEnum |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dfac02887d8f66066a11674ca6dded410df709aa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
指定一个或多个属性[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
|常量|值|Description|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|指示提供程序缓存字段值和从缓存中，这样是后续读取。|  
|**adFldFixed**|0x10|指示该字段包含固定长度的数据。|  
|**adFldIsChapter**|0x2000|指示该字段包含章值，该值指定与此父字段相关的特定子记录集。 通常章字段用于调整数据或筛选器。|  
|**adFldIsCollection**|0x40000|指示该字段指定将记录表示的资源是集合的其他资源，例如文件夹、 而不是简单的资源，例如文本文件。|  
|**adFldKeyColumn**|0x8000|指示该字段指定列的主键的全部或部分。|  
|**adFldIsDefaultStream**|0x20000|指示该字段包含将记录所表示的资源的默认流。 例如，默认流可以在网站上，指定根 URL 时，会自动提供这些根文件夹的 HTML 内容。|  
|**adFldIsNullable**|0x20|指示字段接受 null 值。|  
|**adFldIsRowURL**|0x10000|指示该字段包含名称从数据存储将记录表示资源的 URL。|  
|**adFldLong**|0x80|指示该字段是长度的二进制字段。 此外指示你可以使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)和[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)方法。|  
|**adFldMayBeNull**|0x40|指示你可以从该字段读取 null 值。|  
|**adFldMayDefer**|0x2|指示字段延迟-也就是说，字段值不检索从数据源与整个记录，但仅在显式访问时。|  
|**adFldNegativeScale**|0x4000|指示该字段从支持负的刻度值的列中表示的数字值。 指定刻度[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)属性。|  
|**adFldRowID**|0x100|指示该字段包含一个持久性行标识符，它无法写入且没有有意义的值，若要标识 （如记录号、 唯一标识符，等） 的行除外。|  
|**adFldRowVersion**|0x200|指示该字段包含某种类型的用于跟踪更新的时间或日期戳。|  
|**adFldUnknownUpdatable**|0x8|指示提供程序无法确定是否可以写入该字段。|  
|**adFldUnspecified**|-1 0xFFFFFFFF|指示提供程序未指定字段特性。|  
|**adFldUpdatable**|0x4|指示可以写入该字段。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attributes 属性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|

