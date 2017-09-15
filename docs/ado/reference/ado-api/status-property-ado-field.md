---
title: "状态属性 （ADO 字段） |Microsoft 文档"
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
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65acf492f0364b26fa6a12240fbbd49c7d1dfed3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="status-property-ado-field"></a>状态属性 （ADO 字段）
指示的状态[字段](../../../ado/reference/ado-api/field-object.md)对象。  
  
## <a name="return-value"></a>返回值  
 返回[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)值。 默认值是**adFieldOK**。  
  
## <a name="remarks"></a>注释  
  
## <a name="record-field-status"></a>记录字段状态  
 更改为的值**字段**的字段集合中对象[记录](../../../ado/reference/ado-api/record-object-ado.md)对象缓存之前对象的[更新](../../../ado/reference/ado-api/update-method.md)调用方法。 此时，如果对字段的值的更改导致出现错误，OLE DB 引发错误**DB_E_ERRORSOCCURRED** (2147749409)。 任一种情况的 Status 属性**字段**中的对象**字段**导致错误的集合将包含一个介于[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因此问题。  
  
 若要增强性能、 添加和删除[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合**记录**直到缓存对象**更新**调用方法，以及然后的更改都在批处理开放式更新。 如果**更新**不调用方法，无法更新服务器。 如果任何更新失败则返回 OLE DB 提供程序错误 (DB_E_ERRORSOCCURRED) 和**状态**属性指示的操作和错误状态代码的组合的值。 例如， **adFieldPendingInsert OR adFieldPermissionDenied**。 **状态**每个属性**字段**可以用于确定原因**字段**不添加、 修改或删除。  
  
 许多类型的问题时添加，遇到修改，或删除**字段**通过报告**状态**属性。 例如，如果用户删除**字段**，它已标记为删除**字段**集合。 如果后续**更新**返回错误，因为用户在尝试删除**字段**它们不具有权限，**字段**将具有**状态**的**adFieldPermissionDenied OR adFieldPendingDelete**。 调用[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法还原原始值和集**状态**到**adFieldOK**。  
  
 同样，**更新**方法可能返回错误，因为新**字段**添加，并提供不正确的值。 在该情况下新**字段**将采用**字段**集合的状态和**adFieldPendingInsert** ，也可能**adFieldCantCreate**（具体取决于你的提供商）。 你可以提供适当的值的新**字段**并调用**更新**试。  
  
## <a name="recordset-field-status"></a>记录集字段状态  
 更改为的值**字段**字段集合中的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)缓存之前对象的[更新](../../../ado/reference/ado-api/update-method.md)调用方法。 此时，如果对字段的值的更改导致出现错误，OLE DB 引发错误**DB_E_ERRORSOCCURRED** (2147749409)。 任一种情况的 Status 属性**字段**中的对象**字段**导致错误的集合将包含一个介于[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因此问题。  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [状态属性示例 （字段） (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [状态属性示例 （VC + +）](../../../ado/reference/ado-api/status-property-example-vc.md)   

