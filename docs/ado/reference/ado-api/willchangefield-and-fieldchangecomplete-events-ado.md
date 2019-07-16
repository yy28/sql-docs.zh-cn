---
title: WillChangeField 和 FieldChangeComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7484e2a57925cc22c83456c244dc67aded5cefd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945882"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 和 FieldChangeComplete 事件 (ADO)
**WillChangeField**挂起操作更改的一个或多个值之前，将调用事件[字段](../../../ado/reference/ado-api/field-object.md)中的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **FieldChangeComplete**的一个或多个值后，将调用事件**字段**对象已更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *cFields*  
 一个**长**，该值指示数**字段**中的对象*字段*。  
  
 *Fields*  
 有关**WillChangeField**，则*字段*参数是一个数组**变体**，其中包含**字段**对象的原始值。 有关**FieldChangeComplete**，则*字段*参数是一个数组**变体**，其中包含**字段**具有已更改的值的对象.  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了如果发生的错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**WillChangeField**是调用，此参数设置为**adStatusOK**引发该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消的挂起的操作。  
  
 当**FieldChangeComplete**是调用，此参数设置为**adStatusOK**引发该事件的操作是否成功，或向**adStatusErrorsOccurred**如果操作失败。  
  
 之前**WillChangeField**返回时，将此参数设置为**adStatusCancel**请求取消的挂起的操作。  
  
 之前**FieldChangeComplete**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 一个**记录集**对象。 **记录集**有关发生此事件。  
  
## <a name="remarks"></a>备注  
 一个**WillChangeField**或**FieldChangeComplete**设置时，事件可能会发生[值](../../../ado/reference/ado-api/value-property-ado.md)属性和调用[更新](../../../ado/reference/ado-api/update-method.md)方法使用字段和值的数组参数。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
