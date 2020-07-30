---
title: CancelUpdate 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ecc08dde974826846058d4d8927df202367d28d
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242404"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 方法 (ADO)
在调用[Update](../../../ado/reference/ado-api/update-method.md)方法之前，取消对[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象的当前行或新行所做的任何更改，或[记录](../../../ado/reference/ado-api/record-object-ado.md)对象的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>备注  
  
## <a name="recordset"></a>记录集  
 使用**CancelUpdate**方法可以取消对当前行所做的任何更改，或者放弃新添加的行。 在调用**Update**方法之后，不能取消对当前行或新行所做的更改，除非这些更改是可使用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法回滚的事务的一部分，或者是批处理更新的一部分。 对于批更新，可以使用**CancelUpdate**或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法取消**更新**。  
  
 如果在调用**CancelUpdate**方法时添加新行，则当前行将成为在[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)调用之前的当前行。  
  
 如果处于编辑模式，并且想要移出当前记录（例如，通过使用[move](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)或[Close](../../../ado/reference/ado-api/close-method-ado.md)方法），则可以使用**CancelUpdate**来取消任何挂起的更改。 如果更新无法成功发布到数据源，可能需要执行此操作。 例如，尝试删除因引用完整性冲突而失败时，会在调用[delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)后使**记录集**处于编辑模式。  
  
## <a name="record"></a>Record  
 **CancelUpdate**方法取消[字段](../../../ado/reference/ado-api/field-object.md)对象的任何挂起的插入或删除操作，并取消现有字段的挂起更新并将其还原为原始值。 **字段**集合中所有字段的[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性都设置为**adFieldOK**。  
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [Update 和 CancelUpdate 方法示例（VB）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法示例（VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法（ADO）](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 方法（ADO）](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
