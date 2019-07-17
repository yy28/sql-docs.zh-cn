---
title: UpdateBatch 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9d74fe938ce486a4cd15573af8166dbed12ba6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937844"
---
# <a name="updatebatch-method"></a>UpdateBatch 方法
将所有挂起的批更新写入到磁盘。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 可选。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值指示记录数**UpdateBatch**方法将会影响。  
  
 *PreserveStatus*  
 可选。 一个**布尔**值，该值指定是否本地更改，如所示[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性，应在提交。 如果此值设置为 **，则返回 True**，则**状态**更新完成后，每个记录属性保持不变。  
  
## <a name="remarks"></a>备注  
 使用**UpdateBatch**方法时修改**记录集**批更新模式下传输中所做的所有更改对象**记录集**到基础数据库对象。  
  
 如果**记录集**对象支持批量更新，你可以本地直到你调用缓存到一个或多个记录的多个更改**UpdateBatch**方法。 如果正在编辑当前记录或添加新记录，在调用时**UpdateBatch**方法，将自动调用 ADO[更新](../../../ado/reference/ado-api/update-method.md)方法将任何挂起的更改保存到之前的当前记录传输批的更改为提供程序。 你应使用批处理使用 keyset 或 static 游标仅更新。  
  
> [!NOTE]
>  指定**adAffectGroup**因为中当前没有可见的记录时，此参数的值会导致错误**记录集**（如没有记录与匹配的筛选器）。  
  
 如果尝试将更改传输将因与基础数据发生冲突而失败的任何或所有记录 （例如，一条记录已由另一个用户删除），访问接口将返回到的警告[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合和一个发生运行时错误。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性 (**adFilterAffectedRecords**) 和[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性来查找有冲突的记录。  
  
 若要取消所有挂起的批处理更新，请使用[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)并[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)设置的动态属性，并**记录集**是执行多个表的联接操作的结果则执行**UpdateBatch**方法隐式跟[重新同步](../../../ado/reference/ado-api/resync-method.md)方法，具体取决于设置[Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)属性。  
  
 在数据源执行批处理的各个更新的顺序不一定是执行的本地的顺序相同**记录集**。 更新顺序是取决于提供程序。 考虑到这一点进行编码相关的如外键约束在插入或更新的更新。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [UpdateBatch 和 CancelBatch 方法示例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法示例 （VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 属性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
