---
title: "UpdateBatch 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57c85b6ed83792e2e489eb91dab59bd0da598939
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updatebatch-method"></a>UpdateBatch 方法
将写入磁盘的所有挂起的批更新。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 可选。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值指示多少个记录**UpdateBatch**方法将会影响。  
  
 *PreserveStatus*  
 可选。 A**布尔**值，该值指定是否本地更改，如所示[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性，应将其提交。 如果此值设置为**True**、**状态**在更新完成后，每个记录的属性保持不变。  
  
## <a name="remarks"></a>注释  
 使用**UpdateBatch**方法修改时**记录集**在批处理更新模式下传输中所做的所有更改的对象**记录集**到基础数据库对象。  
  
 如果**记录集**对象支持批处理更新，你可以本地直到你调用缓存到一个或多个记录的多个更改**UpdateBatch**方法。 如果你要编辑的当前记录或添加一条新记录，当你调用**UpdateBatch**方法时，将自动调用 ADO[更新](../../../ado/reference/ado-api/update-method.md)方法将任何挂起的更改保存到之前的当前记录传输到提供程序的批处理的更改。 你应使用批处理使用的键集或仅静态游标更新。  
  
> [!NOTE]
>  指定**adAffectGroup**因为中当前没有可见的记录时，此参数的值将导致错误**记录集**（如没有记录与匹配的筛选器）。  
  
 如果尝试将更改传输由于与基础数据发生冲突而失败的任何或所有记录 （例如，记录已由另一个用户删除），该提供程序返回警告记录到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合和发生运行时错误。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性 (**adFilterAffectedRecords**) 和[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可以查找具有冲突的记录。  
  
 若要取消所有挂起的批处理更新，请使用[执行](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)设置动态属性，与**记录集**是执行对多个表的联接操作的结果则执行**UpdateBatch**方法隐式跟[重新同步](../../../ado/reference/ado-api/resync-method.md)方法，具体取决于的设置[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)属性。  
  
 在数据源执行的批次的各个更新的顺序不一定与执行本地的顺序相同**记录集**。 更新顺序是取决于提供程序。 考虑这在编写代码与另一个，如外键约束上插入或更新相关的更新时。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [UpdateBatch 和执行方法示例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和执行方法示例 （VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [执行方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)

