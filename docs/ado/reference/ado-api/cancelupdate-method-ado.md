---
title: CancelUpdate 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c9320afb2592a37360d65b4645eb68a999a21db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600075"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate 方法 (ADO)
取消对当前或新的行进行任何更改[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，然后才能调用[更新](../../../ado/reference/ado-api/update-method.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>备注  
  
## <a name="recordset"></a>记录集  
 使用**CancelUpdate**方法取消对当前行所做的任何更改或丢弃新添加的行。 调用后，无法取消对当前行或新行的更改**更新**方法，除非所做的更改，可以使用回滚的事务的一部分，否则[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法或部分批量更新。 在批处理更新的情况下，你可以取消**更新**与**CancelUpdate**或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果在调用时，你要添加新行**CancelUpdate**方法，将成为当前行的行之前的当前[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)调用。  
  
 如果你处于编辑模式并想要离开当前记录 (例如，通过使用[移动](../../../ado/reference/ado-api/move-method-ado.md)， [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法)，可以使用**CancelUpdate**取消任何挂起的更改。 您可能需要执行此操作，如果更新不能成功发布到数据源。 例如，尝试删除失败由于引用完整性冲突将离开**记录集**处于编辑模式后调用[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)。  
  
## <a name="record"></a>录制  
 **CancelUpdate**方法取消任何挂起的插入或删除[字段](../../../ado/reference/ado-api/field-object.md)对象，并取消挂起的现有字段的更新并将其还原为其原始值。 [状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性中的所有字段**字段**集合设置为**adFieldOK**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [Update 和 CancelUpdate 方法示例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法示例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
