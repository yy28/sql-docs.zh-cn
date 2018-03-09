---
title: "PageCount 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0ce12f42693b58a57ecc4a08c186027a054bc80
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="pagecount-property-ado"></a>PageCount 属性 (ADO)
指示的数据的多少页面[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象包含。  
  
## <a name="return-value"></a>返回值  
 返回**长**值，该值指示页面在数**记录集**。  
  
## <a name="remarks"></a>注释  
 使用**PageCount**属性来确定多少页的数据位于**记录集**对象。 *页*是一组记录其大小等于[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性设置。 即使的最后一页是不完整，因为有较少的记录，比**PageSize**值，它将计为中的其他页**PageCount**值。 如果**记录集**对象不支持此属性，值将为-1 以指示**PageCount**是无法确定。  
  
 请参阅**PageSize**和[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性上的多个页面功能。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AbsolutePage、 PageCount，以及 PageSize 属性示例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount 和 PageSize 属性示例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 属性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
