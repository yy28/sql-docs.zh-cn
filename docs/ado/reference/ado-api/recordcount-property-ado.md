---
title: RecordCount 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7304062298a95406a223ba58026379a3bebf392f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931471"
---
# <a name="recordcount-property-ado"></a>RecordCount 属性 (ADO)

指示中的记录数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。
  
## <a name="return-value"></a>返回值

返回**长**值，该值指示中的记录数**记录集**。
  
## <a name="remarks"></a>备注

使用**RecordCount**属性来找出的记录数处于**记录集**对象。 该属性返回-1 时 ADO 无法确定的记录数，或提供程序或游标类型不支持**RecordCount**。 读取**RecordCount**属性对已关闭**记录集**将导致错误。

#### <a name="bookmarks-or-approximate-positioning"></a>书签或近似定位

如果记录集对象*does*支持任一书签或近似定位，此属性在记录集中返回的记录的精确数目。 此属性返回而不考虑是否记录集已完全填充的精确数目。

相反，如果该记录集对象的功能*不*支持书签或近似定位，访问此属性可能会大量消耗资源。 流失出现的原因的所有记录，必须检索和计数以返回精确 RecordCount 的值。

- **adBookmark**与书签相关。
- **adApproxPosition**与近似位置。

> [!NOTE]
> 在 ADO 版本 2.8 和更早版本中，SQLOLEDB 访问接口提取所有记录，使用服务器端游标时，它将返回尽管 **，则返回 True**两个**支持 (adApproxPosition)** 并**支持 (adBookmark)** 。
  
游标类型的**记录集**对象会影响是否可确定记录数。 **RecordCount**属性将返回-1 的只进游标; 对于静态的实际计数或键集游标; 或者为-1 或动态游标，具体取决于数据源的实际计数。
  
## <a name="applies-to"></a>适用范围

[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅

[Filter 和 RecordCount 属性示例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter 和 RecordCount 属性示例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
