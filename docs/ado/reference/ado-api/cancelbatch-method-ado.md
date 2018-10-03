---
title: CancelBatch 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c8f0268a91b66f6f26eec1d87502355a1c9795a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828385"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch 方法 (ADO)
取消挂起的批更新。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 可选。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值指示记录数**CancelBatch**方法将会影响。  
  
## <a name="remarks"></a>备注  
 使用**CancelBatch**方法来取消任何挂起的更新中[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)批更新模式中。 如果**记录集**立即更新模式下，调用**CancelBatch**而无需**adAffectCurrent**生成一个错误。  
  
 如果正在编辑当前记录或调用时要添加新记录**CancelBatch**，ADO 首次调用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法取消任何缓存的更改。 在此之后，所有挂起的更改**记录集**已取消。  
  
 当前记录可能无法确定后**CancelBatch**调用，尤其是如果您正在添加新记录。 出于此原因，它是比较明智的做法将当前记录位置设置为中的已知位置**记录集**后**CancelBatch**调用。 例如，调用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
 如果尝试取消挂起的更新将因与基础数据 （例如，如果已由另一个用户删除了记录） 发生冲突而失败，访问接口将返回警告记录到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不会停止程序执行。 仅当在所有请求的记录上不存在冲突，将发生运行时错误。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性 (**adFilterAffectedRecords**) 和[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性来查找有冲突的记录。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [UpdateBatch 和 CancelBatch 方法示例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法示例 （VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
