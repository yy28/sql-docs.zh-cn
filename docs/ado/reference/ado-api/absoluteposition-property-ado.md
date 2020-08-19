---
description: AbsolutePosition 属性 (ADO)
title: " (ADO) 的 AbsolutePosition 属性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e406012b917dd6e1694f5914088bac09201ff99e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451749"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 属性 (ADO)
指示 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md) 对象的当前记录的序号位置。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 对于32位代码，设置或返回 ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)) 的**记录集**对象中的记录数的**长整型**值，或返回[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值之一。  
  
 对于64位代码，请使用提供的数据类型来存储64位值。 例如，你可以使用 Long 或其他64位长度的值，例如 DBORDINAL。 不要使用 **PositionEnum** 值，因为它们限制为32位长度。  
  
## <a name="remarks"></a>备注  
 为了设置 **AbsolutePosition** 属性，ADO 要求使用的 OLE DB 提供程序实现 [IRowsetLocate： IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) 接口。  
  
 访问使用只进或动态游标打开的**记录集**的**AbsolutePosition**属性时，将引发错误**adErrFeatureNotAvailable**。 对于其他游标类型，只要 OLE DB 提供程序支持 **IRowsetScroll： IRowsetLocate** 接口，就会返回正确的位置。 如果提供程序不支持 **IRowsetScroll** 接口，则将属性设置为 **adPosUnknown**。 请参阅提供程序的文档，以确定它是否支持 **IRowsetScroll**。  
  
 使用 **AbsolutePosition** 属性可以根据记录在 **Recordset** 对象中的序号位置移动到记录，也可以确定当前记录的序号位置。 提供程序必须支持适当的功能，此属性才可用。  
  
 与[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)属性类似，当当前记录是**记录集**的第一条记录时， **AbsolutePosition**是从1开始的，等于1。 您可以从[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性中获取**记录集**对象中的记录总数。  
  
 设置 **AbsolutePosition** 属性时，即使该属性是对当前缓存中的记录的设置，ADO 也将使用您指定的记录开头的一组新记录重新加载缓存。 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)属性确定此组的大小。  
  
> [!NOTE]
>  不应将 **AbsolutePosition** 属性用作代理项记录号。 删除前面的记录后，给定记录的位置会发生更改。 如果重新查询或重新打开**Recordset**对象，也不保证给定的记录将具有相同的**AbsolutePosition** 。 书签仍是保留并返回到给定位置的建议方法，是在所有类型的 **Recordset** 对象中定位的唯一方法。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AbsolutePosition 和 CursorLocation 属性示例 (VB) ](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 和 CursorLocation 属性示例 (VC + +) ](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 属性 (ADO) ](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 属性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
