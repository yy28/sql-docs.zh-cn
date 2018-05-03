---
title: RecordCount 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 664b21a320e05f450da1b21a8543e7f4204d71dc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="recordcount-property-ado"></a>RecordCount 属性 (ADO)

指示中的记录数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。
  
## <a name="return-value"></a>返回值

返回**长**值，该值指示中的记录数**记录集**。
  
## <a name="remarks"></a>注释

使用**RecordCount**属性来查明多少个记录位于**记录集**对象。 该属性返回-1 时 ADO 无法确定的记录数，或提供程序或光标类型不支持**RecordCount**。 读取**RecordCount**属性关闭**记录集**会导致错误。

#### <a name="bookmarks-or-approximate-positioning"></a>书签或近似定位

如果记录集对象*未*支持任一书签或近似定位，此属性在记录集中返回的记录的精确数目。 此属性返回而不考虑是否记录集已完全填充的精确数目。

相反，如果该记录集对象的功能*不*支持书签或近似定位，请访问此属性可能会大量消耗资源。 使用量，便会出现的所有记录必须检索计数以返回精确的 RecordCount 值。

- **adBookmark**相关的书签。
- **adApproxPosition**与近似定位相关。

> [!NOTE]
> 在 ADO 版本 2.8 及更早版本中，SQLOLEDB 访问接口提取所有记录，当使用服务器端游标时，它将返回的情况下**True**两个**支持 (adApproxPosition)** 和**支持 (adBookmark)**。
  
游标类型的**记录集**对象会影响是否可以确定的记录数。 **RecordCount**属性将返回-1 表示只进游标; 输入一个静态的实际计数或键集游标; 或者为-1 或动态游标，具体取决于数据源的实际计数。
  
## <a name="applies-to"></a>适用范围

[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅

[筛选器和 RecordCount 属性示例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[筛选器和 RecordCount 属性示例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
