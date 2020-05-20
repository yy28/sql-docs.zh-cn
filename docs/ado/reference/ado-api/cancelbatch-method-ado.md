---
title: CancelBatch 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: rothja
ms.author: jroth
ms.openlocfilehash: c2e9f3b57137b4c113b9e177e9fecefec4070ac0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763168"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch 方法 (ADO)
取消挂起的批更新。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>参数  
 *AffectRecords*  
 可选。 一个[AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，指示**CancelBatch**方法将影响的记录数。  
  
## <a name="remarks"></a>备注  
 使用**CancelBatch**方法可取消批处理更新模式中[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)的任何挂起的更新。 如果**记录集**处于立即更新模式，则在没有**adAffectCurrent**的情况下调用**CancelBatch**将生成错误。  
  
 如果要编辑当前记录或在调用**CancelBatch**时添加新记录，ADO 首先会调用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法来取消任何缓存的更改。 之后，**记录集中**的所有挂起的更改都将被取消。  
  
 当前记录可以在**CancelBatch**调用后无法确定，尤其是在您正在添加新记录的过程中。 出于此原因，将当前记录位置设置为**CancelBatch**调用后**记录集中**的已知位置是明智的。 例如，调用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
 如果由于与基础数据冲突（例如，如果另一记录已被其他用户删除）而导致取消挂起更新的尝试失败，则该提供程序会将警告返回到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不会暂停程序执行。 仅当所有请求的记录上发生冲突时才会发生运行时错误。 使用[Filter](../../../ado/reference/ado-api/filter-property.md)属性（**AdFilterAffectedRecords**）和[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可查找存在冲突的记录。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [UpdateBatch 和 CancelBatch 方法示例（VB）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法示例（VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel 方法（ADO）](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear 方法（ADO）](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 属性（ADO）](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
