---
title: "Delete 方法 （ADO 记录集） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords: Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ff78b2827f8bd6aa22ded6429f0468617b7a83d9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="delete-method-ado-recordset"></a>Delete 方法 （ADO 记录集）
删除当前记录或一组记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值确定多少个记录**删除**方法将会影响。 默认值是**adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll**和**adAffectAllChapters**不是有效的自变量到**删除**。  
  
## <a name="remarks"></a>Remarks  
 使用**删除**方法将当前记录或一组中的记录标记[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象以备删除。 如果**记录集**对象不允许记录删除，将会出错。 如果要立即更新模式中，删除数据库中会立即发生。 如果无法成功删除记录 （由于数据库完整性的冲突，例如），该记录将保持处于编辑模式的调用后[更新](../../../ado/reference/ado-api/update-method.md)。 这意味着你必须取消的更新[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)之前离开当前记录 (例如，对于[关闭](../../../ado/reference/ado-api/close-method-ado.md)，[移动](../../../ado/reference/ado-api/move-method-ado.md)，或[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果要在批处理更新模式下，记录将被标记为从缓存中删除，当你调用，时会发生实际删除[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性以查看已删除的记录。  
  
 从已删除的记录中检索字段值将生成错误。 删除当前记录后, 已删除的记录仍保留当前直到移动到另一条记录。 一旦离开已删除的记录，它将不再可访问。  
  
 如果嵌套在事务中的删除，则可以恢复已删除的记录与[不](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果要在批处理更新模式下，你可以取消的挂起的删除或组的挂起的删除与[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果尝试删除记录失败，因为与基础数据有冲突 （例如，记录已由另一个用户删除），该提供程序返回警告记录到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合但不会停止程序执行。 只有在所有请求的记录上冲突，则会发生运行时错误。  
  
 如果[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)设置动态属性，则与**记录集**是执行对多个表的联接操作的结果则**删除**方法将仅删除在名为的表中的行[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)属性。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [删除方法示例 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [删除方法示例 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [删除方法示例 （VC + +）](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
