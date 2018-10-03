---
title: 状态属性 （ADO 字段） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11a39cf6f30e7a4892d6f2df5c8c373ab6847632
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741515"
---
# <a name="status-property-ado-field"></a>Status 属性（ADO 字段）
指示的状态[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)值。 默认值是**adFieldOK**。  
  
## <a name="remarks"></a>备注  
  
## <a name="record-field-status"></a>记录字段状态  
 值将变为**字段**的字段集合中对象[记录](../../../ado/reference/ado-api/record-object-ado.md)直到该对象的缓存对象[更新](../../../ado/reference/ado-api/update-method.md)调用方法。 此时，如果对字段的值的更改导致的错误，OLE DB 将引发错误**DB_E_ERRORSOCCURRED** (2147749409)。 Status 属性的任一**字段**中的对象**字段**导致了错误的集合将包含值[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因出现问题。  
  
 若要增强性能、 添加和删除[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合**记录**直到缓存对象**更新**调用方法时，以及然后的更改在批处理优化更新中进行。 如果**更新**不会调用方法时，不更新服务器。 如果任何更新失败，则返回 OLE DB 提供程序出错 (DB_E_ERRORSOCCURRED) 和**状态**属性指示的组合的值的操作和错误状态代码。 例如， **adFieldPendingInsert OR adFieldPermissionDenied**。 **状态**属性为每个**字段**可用于确定为什么**字段**不添加、 修改或删除。  
  
 许多类型的问题时添加，遇到修改或删除**字段**通过报告**状态**属性。 例如，如果用户删除**字段**，它标记为删除从**字段**集合。 如果后续**更新**将返回错误，因为用户尝试删除**字段**他们不具有权限，**字段**将具有**状态**的**adFieldPermissionDenied OR adFieldPendingDelete**。 调用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法还原原始值和集**状态**到**adFieldOK**。  
  
 同样，**更新**方法可能返回错误，因为新**字段**已添加并给出不适当的值。 在该示例中的新**字段**位于**字段**集合和有状态**adFieldPendingInsert** ，也可能**adFieldCantCreate**（具体取决于您的提供程序）。 你可以提供适当的值的新**字段**，并调用**更新**试。  
  
## <a name="recordset-field-status"></a>记录集字段状态  
 值将变为**字段**的字段集合中对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)直到该对象的缓存[更新](../../../ado/reference/ado-api/update-method.md)调用方法。 此时，如果对字段的值的更改导致的错误，OLE DB 将引发错误**DB_E_ERRORSOCCURRED** (2147749409)。 Status 属性的任一**字段**中的对象**字段**导致了错误的集合将包含值[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因出现问题。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Status 属性示例 （字段） (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [State 属性示例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
