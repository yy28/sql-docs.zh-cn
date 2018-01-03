---
title: "重新同步方法 |Microsoft 文档"
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
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords: Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 101e2695a47b2c255aac94aedb6b613c1fca15c6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="resync-method"></a>重新同步方法
刷新当前中的数据[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，从基础数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 可选。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值确定多少个记录**重新同步**方法将会影响。 默认值是**adAffectAll**。 此值不可用**重新同步**方法**字段**集合**记录**对象。  
  
 *ResyncValues*  
 可选。 A [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)值，该值指定是否覆盖基础值。 默认值是**adResyncAllValues**。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="recordset"></a>记录集  
 使用**重新同步**方法重新同步在当前记录**记录集**与基础数据库。 如果你使用的静态或只进游标，但你想要查看基础数据库中的任何更改，这非常有用。  
  
 如果你设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**，**重新同步**功能仅适用于非只读**记录集**对象。  
  
 与不同[Requery](../../../ado/reference/ado-api/requery-method.md)方法，**重新同步**方法不会重新执行**记录集**对象的基本命令。 基础数据库中的新记录将不可见。  
  
 如果尝试重新同步将失败，因为与基础数据有冲突 （例如，记录已由另一个用户），该提供程序返回警告记录到[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合中，运行时错误时发生。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性 (**adFilterConflictingRecords**) 和[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可以查找具有冲突的记录。  
  
 如果[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)设置动态属性，与**记录集**是执行多个表，则联接运算的结果**重新同步**方法将执行命令中给定**重新同步命令**属性仅在中名为的表上**唯一表**属性。  
  
## <a name="fields"></a>字段  
 使用**重新同步**方法重新同步的值**字段**集合**记录**与基础数据源的对象。 [计数](../../../ado/reference/ado-api/count-property-ado.md)属性不受此方法。  
  
 如果*ResyncValues*设置为**adResyncAllValues** （默认值）， [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)，[值](../../../ado/reference/ado-api/value-property-ado.md)，和[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)属性[字段](../../../ado/reference/ado-api/field-object.md)同步对集合中的对象。 如果*ResyncValues*设置为**adResyncUnderlyingValues**，则只**UnderlyingValue**同步属性。  
  
 值**状态**每个属性**字段**对象时的调用还会影响的行为**重新同步**。 有关**字段**对象具有**状态**值**adFieldPendingUnknown**或**adFieldPendingInsert**，**重新同步**不起作用。 有关**状态**值**adFieldPendingChange**或**adFieldPendingDelete**，**重新同步**同步字段的数据值，数据源中仍存在。  
  
 **重新同步**将不会修改**状态**值**字段**对象，除非发生错误时**重新同步**调用。 例如，如果该字段不再存在，提供程序将返回相应**状态**值**字段**对象，如**adFieldDoesNotExist**。 返回**状态**值可以进行逻辑组合的值中**状态**属性。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [重新同步方法示例 (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [重新同步方法示例 （VC + +）](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 属性](../../../ado/reference/ado-api/underlyingvalue-property.md)
