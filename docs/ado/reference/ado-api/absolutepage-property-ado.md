---
title: AbsolutePage 属性 (ADO) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921834"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 属性 (ADO)
指示当前记录驻留在哪一页。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 对于 32 位代码，设置或返回**长**介于 1 和中的页数[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象 ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md))，或返回的一个[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 对于 64 位代码，使用提供的 64 位值存储的数据类型。 例如，可以使用任一**长**或另一个值，该值可如 DBORDINAL 64 位长度。 不要使用**PositionEnum**值，因为它们被限制为 32 位长度。  
  
## <a name="remarks"></a>备注  
 此属性可以用于确定当前记录所在的页号。 它使用[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性将从逻辑上划分的总的行集计数**记录集**对象的一系列页面，其中每个记录等于数**PageSize**（除最后一页，其中可能有较少的记录）。 提供程序必须支持相应的功能，此属性才可用。  
  
-   获取或设置时**AbsolutePage**属性，将使用 ADO [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)属性并[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)属性一起，如下所示：  
  
-   若要获取**AbsolutePage**，ADO 首先检索**AbsolutePosition**，然后，它通过将**PageSize**。  
  
-   若要设置**AbsolutePage**，ADO 移动**AbsolutePosition** ，如下所示： 将其乘以**PageSize**通过新**AbsolutePage**值，然后将 1 添加到值。 因此，当前放置**记录集**已成功设置后**AbsolutePage**是该页面中的第一个记录。  
  
 像**AbsolutePosition**属性， **AbsolutePage**是基于 1 的和等于 1 时的当前记录中的第一个记录**记录集**。 设置此属性将移动到特定页面的第一个记录。 获取从总页数**PageCount**属性。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [AbsolutePage、 PageCount、 和 PageSize 属性示例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount、 和 PageSize 属性示例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 属性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 属性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
