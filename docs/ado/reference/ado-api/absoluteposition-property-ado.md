---
title: AbsolutePosition 属性 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 615bbf4f771d6d3b12edfec3184ef0ee091fbe08
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274986"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 属性 (ADO)
指示的序号位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的当前记录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 对于 32 位代码中，设置或返回**长**介于 1 和中的记录数值**记录集**对象 ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md))，或返回类型之一[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 对于 64 位代码，使用提供的存储的 64 位值的数据类型。 例如，可以使用 long 类型的值或另一个值，该值是如 DBORDINAL 的 64 位长度。 不要使用**PositionEnum**值因为它们限制为 32 位长度。  
  
## <a name="remarks"></a>Remarks  
 若要设置**AbsolutePosition**属性，ADO 需要你使用的 OLE DB 访问接口实现[IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx)接口。  
  
 访问**AbsolutePosition**属性**记录集**打开过使用只进动态游标引发错误或**adErrFeatureNotAvailable**。 与其他游标类型，正确的位置将具有如只要的 OLE DB 访问接口支持的返回**IRowsetScroll:IRowsetLocate**接口。 如果提供程序不支持**IRowsetScroll**接口，该属性设置为**adPosUnknown**。 请参阅您的提供程序，以确定它是否支持文档**IRowsetScroll**。  
  
 使用**AbsolutePosition**要移动到记录属性基于其序号位置**记录集**对象，或者想要确定当前记录的序号位置。 提供程序必须支持相应的功能，此属性才可用。  
  
 如[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性， **AbsolutePosition**是基于 1 的并且等于 1 时的当前记录是中的第一个记录**记录集**。 你可以获取的中的记录总数**记录集**对象[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性。  
  
 当你将设置**AbsolutePosition**属性，即使它是当前的缓存中中的记录 ADO 将重新加载缓存与新的组的开头你指定的记录的记录。 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)属性确定此组的大小。  
  
> [!NOTE]
>  不应使用**AbsolutePosition**属性作为代理项记录号。 当删除前一条记录时，将更改给定的记录的位置。 此外没有给定的记录将具有相同不保证**AbsolutePosition**如果**记录集**重新查询对象或将其重新打开。 书签仍然保留，并返回到给定位置的推荐的方法，而且是适用于的所有类型的定位的唯一方式**记录集**对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [AbsolutePosition 和 CursorLocation 属性示例 (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 和 CursorLocation 属性示例 （VC + +）](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
