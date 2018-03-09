---
title: "正在执行方法 (ADO) |Microsoft 文档"
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
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd858ec4d40f307027a75fa657c4e4d2b0539064
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="cancelupdate-method-ado"></a>正在执行方法 (ADO)
取消对当前或新的行进行任何更改[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，然后再调用[更新](../../../ado/reference/ado-api/update-method.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>注释  
  
## <a name="recordset"></a>记录集  
 使用**正在执行**方法可取消对当前行进行任何更改，或放弃新添加的行。 您无法取消对当前行或新行的更改后调用**更新**方法，除非所做的更改是你可以回滚，事务的任一一部分[不](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法或部分批量更新。 对于批处理更新时，你可以取消**更新**与**正在执行**或[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果在调用时，要添加新行**正在执行**方法，当前行变成之前的当前行[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)调用。  
  
 如果你处于编辑模式，并想要离开当前记录 (例如，通过使用[移动](../../../ado/reference/ado-api/move-method-ado.md)，[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法)，你可以使用**正在执行**取消任何挂起的更改。 你可能需要执行此操作，如果更新不能成功发布到数据源。 例如，尝试删除失败由于违反了引用完整性而将保留**记录集**在编辑模式下调用了[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)。  
  
## <a name="record"></a>記錄  
 **正在执行**方法取消任何挂起的插入或删除[字段](../../../ado/reference/ado-api/field-object.md)对象，并取消挂起的现有字段的更新并将它们还原到其原始值。 [状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性中的所有字段**字段**集合设置为**adFieldOK**。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [更新和正在执行的方法示例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [更新和正在执行的方法示例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [执行方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [正在执行方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
