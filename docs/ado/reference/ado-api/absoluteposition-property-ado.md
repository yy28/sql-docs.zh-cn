---
title: AbsolutePosition 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4444c54df6e3629e7f69e3fe0d54625f66c3e703
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813155"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 属性 (ADO)
指示的序号位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的当前记录。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 对于 32 位代码，设置或返回**长**介于 1 到中的记录数的值**记录集**对象 ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md))，或返回的一个[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 对于 64 位代码，使用提供的 64 位值存储的数据类型。 例如，可以使用长时间或另一个值，它是如 DBORDINAL 64 位长度。 不要使用**PositionEnum**因为它们限制为 32 位长度的值。  
  
## <a name="remarks"></a>备注  
 若要设置**AbsolutePosition**属性，ADO 需要您使用的 OLE DB 提供程序实现[IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx)接口。  
  
 访问**AbsolutePosition**的属性**记录集**只进打开使用或动态游标会引发错误**adErrFeatureNotAvailable**。 对于其他游标的类型，正确的位置将会返回，只要 OLE DB 访问接口支持**IRowsetScroll:IRowsetLocate**接口。 如果提供程序不支持**IRowsetScroll**接口，该属性设置为**adPosUnknown**。 请参阅您的提供商以确定它是否支持的文档**IRowsetScroll**。  
  
 使用**AbsolutePosition**属性将移动到一条记录根据其序号位置**记录集**对象，或者想要确定当前记录的序号位置。 提供程序必须支持相应的功能，此属性才可用。  
  
 像[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性， **AbsolutePosition**是基于 1 的和等于 1 时的当前记录中的第一个记录**记录集**。 你可以获取的中的记录总数**记录集**对象从[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性。  
  
 当您将设置**AbsolutePosition**属性，即使它是与当前缓存中的记录 ADO 重新加载缓存，通过从指定的记录的记录的新组。 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)属性来确定此组的大小。  
  
> [!NOTE]
>  不应使用**AbsolutePosition**属性作为代理项记录号。 在给定的记录发生更改时删除前一条记录的位置。 此外，还有不保证给定的记录将具有相同**AbsolutePosition**如果**记录集**重新查询对象或将其重新打开。 书签是仍保留和返回到给定位置的推荐的方法而且这是唯一的定位跨所有类型的方法**记录集**对象。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [AbsolutePosition 和 CursorLocation 属性示例 (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 和 CursorLocation 属性示例 （VC + +）](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
