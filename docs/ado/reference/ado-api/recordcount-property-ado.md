---
title: "RecordCount 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 402a481ef7db03e2d7197eb02010a1c93b974570
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="recordcount-property-ado"></a>RecordCount 属性 (ADO)
指示中的记录数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值指示中的记录数**记录集**。  
  
## <a name="remarks"></a>注释  
 使用**RecordCount**属性来查明多少个记录位于**记录集**对象。 该属性返回-1 时 ADO 无法确定的记录数，或提供程序或光标类型不支持**RecordCount**。 读取**RecordCount**属性关闭**记录集**会导致错误。  
  
 如果**记录集**对象支持近似定位或创建一个书签，??? 也就是说，**支持 (adApproxPosition)**或**支持 (adBookmark)**分别返回**True**??? 此值将为中的记录的精确数目**记录集**，不管是否它已完全填充。 如果**记录集**对象不支持近似定位，此属性可能是大量消耗资源，因为所有记录都将都具有检索和计数以返回准确**RecordCount**值。  
  
> [!NOTE]
>  在 ADO 版本 2.8 及更早版本中，SQLOLEDB 访问接口提取所有记录，当使用服务器端游标时，它将返回的情况下**True**两个**支持 (adApproxPosition)**和**支持 (adBookmark)**。  
  
 游标类型的**记录集**对象会影响是否可以确定的记录数。 **RecordCount**属性将返回-1 表示只进游标; 输入一个静态的实际计数或键集游标; 或者为-1 或动态游标，具体取决于数据源的实际计数。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [筛选器和 RecordCount 属性示例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [筛选器和 RecordCount 属性示例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

