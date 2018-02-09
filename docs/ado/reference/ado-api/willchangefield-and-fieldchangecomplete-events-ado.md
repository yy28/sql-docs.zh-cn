---
title: "WillChangeField 和 FieldChangeComplete 事件 (ADO) |Microsoft 文档"
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
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 98b5b27b9a6111768f2ef2c5e9470b4b87fa9acc
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 和 FieldChangeComplete 事件 (ADO)
**WillChangeField**挂起的操作更改一个或多个值之前，将调用事件[字段](../../../ado/reference/ado-api/field-object.md)中的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **FieldChangeComplete**事件时调用一个或多个值后**字段**对象已更改。  
  
## <a name="syntax"></a>语法  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *cFields*  
 A**长**，该值指示数**字段**中的对象*字段*。  
  
 *Fields*  
 有关**WillChangeField**、*字段*参数是数组的**变体**包含**字段**对象的原始值。 有关**FieldChangeComplete**、*字段*参数是数组的**变体**包含**字段**具有已更改的值的对象.  
  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值*adStatus*是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**WillChangeField**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消挂起操作。  
  
 当**FieldChangeComplete**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功，或到**adStatusErrorsOccurred**如果操作失败。  
  
 之前**WillChangeField**返回时，将此参数设置为**adStatusCancel**的请求取消的挂起的操作。  
  
 之前**FieldChangeComplete**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 A**记录集**对象。 **记录集**此事件发生的。  
  
## <a name="remarks"></a>注释  
 A **WillChangeField**或**FieldChangeComplete**设置时，事件可能会发生[值](../../../ado/reference/ado-api/value-property-ado.md)属性和调用[更新](../../../ado/reference/ado-api/update-method.md)方法具有字段和值的数组参数。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
