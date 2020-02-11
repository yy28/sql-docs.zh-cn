---
title: AbsolutePage 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12b2e6c6f12fc06cb223551b55cb7f9a38df9ac3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921834"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 属性 (ADO)
指示当前记录所在的页。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 对于32位代码，设置或返回一个从1到[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象（[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)）中的页数的**长**值，或返回[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值之一。  
  
 对于64位代码，请使用提供的数据类型来存储64位值。 例如，你可以使用**Long**或其他64值（如 DBORDINAL）。 不要使用**PositionEnum**值，因为它们限制为32位长度。  
  
## <a name="remarks"></a>备注  
 此属性可用于标识当前记录所在的页码。 它使用[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性以逻辑方式将**记录集**对象的总行集计数划分为一系列页，其中每个页的记录数等于**PageSize** （可能包含较少记录的最后一页除外）。 提供程序必须支持适当的功能，此属性才可用。  
  
-   获取或设置**AbsolutePage**属性时，ADO 将[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)属性和[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性一起使用，如下所示：  
  
-   若要获取**AbsolutePage**，ADO 首先检索**AbsolutePosition**，然后将其除以**PageSize**。  
  
-   若要设置**AbsolutePage**，ADO 会按如下所示移动**AbsolutePosition** ：它将**PageSize**乘以新的**AbsolutePage**值，然后将1添加到值中。 因此，成功设置**AbsolutePage**后**记录集中**的当前位置是该页中的第一条记录。  
  
 与**AbsolutePosition**属性类似，当当前记录是**记录集**的第一条记录时， **AbsolutePage**是从1开始的，等于1。 设置此属性可以移动到特定页的第一条记录。 获取**PageCount**属性中的总页数。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AbsolutePage、PageCount 和 PageSize 属性示例（VB）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 属性示例（VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 属性（ADO）](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 属性（ADO）](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 属性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
