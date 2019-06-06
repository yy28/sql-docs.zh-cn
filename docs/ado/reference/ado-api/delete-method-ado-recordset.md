---
title: Delete 方法 （ADO 记录集） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fab7baf1771ad0600f4c1a0a8cac931f0adcc0a4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695428"
---
# <a name="delete-method-ado-recordset"></a>Delete 方法（ADO 记录集）
删除当前记录或一组记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值确定的记录数**删除**方法将会影响。 默认值是**adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll**并**adAffectAllChapters**不是有效的参数**删除**。  
  
## <a name="remarks"></a>备注  
 使用**删除**方法将当前记录或一组中的记录标记[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象以备删除。 如果**记录集**对象不允许记录删除，就会出错。 如果要立即更新模式中，删除数据库中立即执行。 如果不能 （由于数据库完整性的冲突，例如） 已成功删除了记录，该记录将保持在编辑模式下调用后面[更新](../../../ado/reference/ado-api/update-method.md)。 这意味着您必须取消的更新[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)之前移出当前记录 (例如，对于[关闭](../../../ado/reference/ado-api/close-method-ado.md)，[移动](../../../ado/reference/ado-api/move-method-ado.md)，或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果要在批更新模式中，记录将被标记为从缓存中删除，并在调用时，会发生实际删除[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)要查看已删除的记录的属性。  
  
 从已删除的记录中检索字段值将生成错误。 删除当前记录后, 已删除的记录保持最新，直到你将移动到另一条记录。 一次您移开的已删除的记录，将不再可访问。  
  
 如果将嵌套在事务中的删除，则可以恢复已删除的记录与[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果要在批更新模式中，可以取消挂起的删除或挂起的删除操作使用的组[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果尝试删除的记录将因与基础数据发生冲突而失败 （例如，一条记录已由另一个用户删除），访问接口将返回到的警告[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不会停止程序执行。 仅当在所有请求的记录上不存在冲突，将发生运行时错误。  
  
 如果[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)动态属性设置，并**记录集**是执行多个表的联接操作的结果则**删除**方法将仅删除中命名的表中的行[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)属性。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Delete 方法示例 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 方法示例 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 方法示例 （VC + +）](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
