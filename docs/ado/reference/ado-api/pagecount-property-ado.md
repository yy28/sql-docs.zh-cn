---
title: PageCount 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5187c73d4dde95a5ddd9396da95b2d4381c868c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706937"
---
# <a name="pagecount-property-ado"></a>PageCount 属性 (ADO)
指示数据的多少页面[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象包含。  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值指示在页数**记录集**。  
  
## <a name="remarks"></a>备注  
 使用**PageCount**属性来确定多少页的数据位于**记录集**对象。 *页面*是一组记录的大小等于[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性设置。 即使最后一页是不完整，因为有比记录更少**PageSize**值，它计为中的其他页**PageCount**值。 如果**记录集**对象不支持此属性，值将为-1 指示**PageCount**是无法确定。  
  
 请参阅**PageSize**并[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)在页的多个功能的属性。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [AbsolutePage、 PageCount、 和 PageSize 属性示例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount、 和 PageSize 属性示例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 属性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
