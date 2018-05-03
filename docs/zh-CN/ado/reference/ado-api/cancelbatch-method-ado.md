---
title: 执行方法 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d0cc416946a658bc48fa4c6f1c94048b94fb71a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="cancelbatch-method-ado"></a>执行方法 (ADO)
取消挂起的批更新。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值指示多少个记录**执行**方法将会影响。  
  
## <a name="remarks"></a>注释  
 使用**执行**方法来取消任何挂起的更新中[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)在批处理更新模式下。 如果**记录集**处于立即更新模式，调用**执行**而无需**adAffectCurrent**生成错误。  
  
 如果你正在编辑当前记录或要添加一条新记录，在调用时**执行**，ADO 第一个调用[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法来取消任何缓存的更改。 在此之后，所有挂起的更改在**记录集**则已取消。  
  
 当前记录可能无法确定后**执行**调用，尤其是如果你在过程中添加一条新记录。 为此，它是比较明智的做法将当前记录位置设置为中的已知位置**记录集**后**执行**调用。 例如，调用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
 如果取消挂起的更新的尝试失败，因为与基础数据 （例如，如果已由另一个用户中删除一条记录） 有冲突，该提供程序返回警告记录到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合但不会停止程序执行。 只有在所有请求的记录上冲突，则会发生运行时错误。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性 (**adFilterAffectedRecords**) 和[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可以查找具有冲突的记录。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [UpdateBatch 和执行方法示例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和执行方法示例 （VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [正在执行方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [正在执行方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
