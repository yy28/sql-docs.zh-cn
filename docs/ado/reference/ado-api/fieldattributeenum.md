---
title: FieldAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80fb27aa51d6e0a44f8f006711708e24cd04bef3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632315"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
指定的一个或多个特性[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|指示提供程序缓存字段值和从缓存，可以完成，后续读取。|  
|**adFldFixed**|0x10|指示该字段包含固定长度的数据。|  
|**adFldIsChapter**|0x2000|指示该字段包含一个章值，该值指定与此父字段相关的特定子记录集。 通常一章字段用于数据整理或筛选器。|  
|**adFldIsCollection**|0x40000|指示该字段指定记录所表示的资源是其他资源，例如文件夹，而不是简单的资源，例如文本文件的集合。|  
|**adFldKeyColumn**|0x8000|指示该字段指定列的主键的全部或部分。|  
|**adFldIsDefaultStream**|0x20000|指示该字段包含由记录表示的资源的默认流。 例如，默认流可以是上一个网站，当指定的根 URL 就会自动提供的根文件夹的 HTML 内容。|  
|**adFldIsNullable**|0x20|指示该字段接受 null 值。|  
|**adFldIsRowURL**|0x10000|指示该字段包含的 URL 的名称将记录表示的数据存储区的资源。|  
|**adFldLong**|0x80|指示该字段的长度的二进制字段。 此外表示可以使用[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)并[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)方法。|  
|**adFldMayBeNull**|0x40|指示可以从该字段读取 null 值。|  
|**adFldMayDefer**|0x2|指示字段延迟 — 也就是说，字段值不会检索从数据源与整个记录，但仅当您显式访问它们。|  
|**adFldNegativeScale**|0x4000|指示该字段从支持负的小数位数值的列表示的数字值。 指定刻度[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)属性。|  
|**adFldRowID**|0x100|指示该字段包含的永久行标识符，无法写入到除若要标识 （例如记录号、 唯一标识符等） 的行没有有意义的值。|  
|**adFldRowVersion**|0x200|指示该字段包含某种类型的用来跟踪更新的时间或日期戳。|  
|**adFldUnknownUpdatable**|0x8|指示提供程序不能确定是否可以写入该字段。|  
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
