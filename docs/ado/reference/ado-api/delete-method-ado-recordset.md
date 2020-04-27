---
title: Delete 方法（ADO 记录集） |Microsoft Docs
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
ms.openlocfilehash: b978e3d885e3ff06dda18859384f88eb4c564254
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919125"
---
# <a name="delete-method-ado-recordset"></a>Delete 方法（ADO 记录集）
删除当前记录或一组记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>参数  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，用于确定**Delete**方法将影响的记录数。 默认值为**adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll**和**adAffectAllChapters**不是要**删除**的有效参数。  
  
## <a name="remarks"></a>备注  
 使用**Delete**方法将当前记录或记录[集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中的一组记录标记为删除。 如果**记录集**对象不允许删除记录，则会发生错误。 如果处于立即更新模式，则会立即删除数据库中的删除操作。 如果无法成功删除记录（例如，由于数据库完整性冲突），则在调用[Update](../../../ado/reference/ado-api/update-method.md)后，该记录将继续处于编辑模式。 这意味着，在离开当前记录（例如，具有[Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)）之前，必须取消[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)的更新。  
  
 如果处于批处理更新模式，记录将标记为从缓存中删除，并且在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法时会发生实际的删除。 使用 "[筛选器](../../../ado/reference/ado-api/filter-property.md)" 属性查看已删除的记录。  
  
 从已删除记录中检索字段值将生成错误。 删除当前记录后，删除的记录将保持当前状态，直到您移到另一记录为止。 离开删除的记录后，它将无法再访问。  
  
 如果在事务中嵌套删除，则可以使用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法恢复已删除的记录。 如果处于批处理更新模式，可以使用[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法取消挂起的删除或挂起的删除组。  
  
 如果由于与基础数据发生冲突而导致删除记录的尝试失败（例如，记录已被其他用户删除），则提供程序会将警告返回到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不会暂停程序执行。 仅当所有请求的记录上发生冲突时才会发生运行时错误。  
  
 如果设置了 "[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)动态" 属性，并且**记录集**是对多个表执行联接操作的结果，则**delete**方法将仅删除 "[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)" 属性中命名的表中的行。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Delete 方法示例（VB）](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 方法示例（VBScript）](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 方法示例（VC + +）](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 方法（ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
