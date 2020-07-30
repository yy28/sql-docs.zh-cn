---
title: 重新同步方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6907bfa9b83370074db9d9e2e522ed49d2c96e7e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243208"
---
# <a name="resync-method"></a>重新同步方法
刷新当前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中的数据，或从基础数据库刷新[记录](../../../ado/reference/ado-api/record-object-ado.md)对象的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合中的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>参数  
 *AffectRecords*  
 可选。 一个[AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，用于确定**Resync**方法将影响的记录数。 默认值为**adAffectAll**。 此值不能用于**Record**对象的 "**字段**" 集合的 "重新**同步**" 方法。  
  
 *ResyncValues*  
 可选。 一个[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)值，该值指定是否覆盖基础值。 默认值为**adResyncAllValues**。  
  
## <a name="remarks"></a>备注  
  
## <a name="recordset"></a>记录集  
 使用 "重新**同步**" 方法可使当前**记录集中**的记录与基础数据库重新同步。 如果你使用的是静态或只进游标，但你想要查看基础数据库中的任何更改，这会很有用。  
  
 如果将[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**，则只能对非只读**记录集**对象进行重新**同步**。  
  
 与[Requery](../../../ado/reference/ado-api/requery-method.md)方法不同， **Resync**方法不会重新执行**Recordset**对象的基础命令。 基础数据库中的新记录将不可见。  
  
 如果尝试重新同步失败是由于与基础数据发生冲突（例如，另一个用户删除了记录），则提供程序将向[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合返回警告，并发生运行时错误。 使用[Filter](../../../ado/reference/ado-api/filter-property.md)属性（**AdFilterConflictingRecords**）和[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性可查找存在冲突的记录。  
  
 如果设置了[唯一的表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[Resync 命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)动态属性，并且**记录集**是对多个表执行联接操作的结果，则**Resync**方法将仅对在**Unique 表**属性中指定的表执行**resync command**属性中给定的命令。  
  
## <a name="fields"></a>字段  
 使用 "重新**同步**" 方法可使**Record**对象的 "**字段**" 集合的值与基础数据源重新同步。 [Count](../../../ado/reference/ado-api/count-property-ado.md)属性不受此方法的影响。  
  
 如果*将 ResyncValues*设置为**adResyncAllValues** （默认值），则将同步集合中[Field](../../../ado/reference/ado-api/field-object.md)对象的[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)、 [value](../../../ado/reference/ado-api/value-property-ado.md)和[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)属性。 如果*ResyncValues*设置为**adResyncUnderlyingValues**，则只同步**UnderlyingValue**属性。  
  
 调用时每个**Field**对象的**Status**属性的值也会影响重新**同步**的行为。 对于**状态**值为**adFieldPendingUnknown**或**adFieldPendingInsert**的**字段**对象，重新**同步**不起作用。 对于**adFieldPendingChange**或**adFieldPendingDelete**的**状态值**， **Resync**同步数据源中仍存在的字段的数据值。  
  
 重新**同步**不会修改**字段**对象的**状态值**，除非在调用重新**同步**时发生错误。 例如，如果该字段不存在，则提供程序将返回**字段**对象的相应**状态值**，如**adFieldDoesNotExist**。 返回的**状态值**可以在 "**状态**" 属性的值中以逻辑方式组合。  
  
## <a name="applies-to"></a>应用到  

:::row:::
    :::column:::
        [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [Resync 方法示例（VB）](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync 方法示例（VC + +）](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 方法（ADO）](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 属性](../../../ado/reference/ado-api/underlyingvalue-property.md)
