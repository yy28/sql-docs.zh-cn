---
title: RecordCount 属性（ADO） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931471"
---
# <a name="recordcount-property-ado"></a>RecordCount 属性 (ADO)

指示[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中的记录数。
  
## <a name="return-value"></a>返回值

返回一个**长整型**值，该值指示记录**集中**的记录数。
  
## <a name="remarks"></a>备注

使用**RecordCount**属性可查看**记录集**对象中的记录数。 如果 ADO 无法确定记录数，或者提供程序或游标类型不支持**RecordCount**，则属性将返回-1。 读取已关闭**记录集**的**RecordCount**属性会导致错误。

#### <a name="bookmarks-or-approximate-positioning"></a>书签或近似定位

如果*recordset 对象支持*书签或近似定位，则此属性将返回记录集中的确切记录数。 无论记录集是否已完全填充，此属性都将返回准确的数字。

与此相反，如果记录集对象*不*支持书签或近似定位，则访问此属性可能会占用大量资源。 发生排出的原因是，所有记录都必须检索到并计入，以返回准确的 RecordCount 值。

- 与书签相关的**adBookmark** 。
- **adApproxPosition**与近似定位相关。

> [!NOTE]
> 在 ADO 版本2.8 及更早版本中，如果使用服务器端游标，则 SQLOLEDB 提供程序将提取所有记录，尽管它对于这两个**支持（adApproxPosition）** 和**支持（adBookmark）** 都返回**True** 。
  
**Recordset**对象的游标类型会影响是否可以确定记录数。 对于只进游标， **RecordCount**属性将返回-1;静态或键集游标的实际计数;和-1 或动态游标的实际计数，具体取决于数据源。
  
## <a name="applies-to"></a>应用于

[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅

[Filter 和 RecordCount 属性示例（VB）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter 和 RecordCount 属性示例（VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 属性（ADO）](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
