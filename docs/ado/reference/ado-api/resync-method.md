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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 251c2f67861dd996ac78efc9a8e599d7ec191072
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711553"
---
# <a name="resync-method"></a>重新同步方法
刷新在当前数据[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，从基础数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parameters  
 *AffectRecords*  
 可选。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，该值确定的记录数**重新同步**方法将会影响。 默认值是**adAffectAll**。 此值不是适用于**重新同步**方法**字段**的集合**记录**对象。  
  
 *ResyncValues*  
 可选。 一个[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)值，该值指定是否覆盖基础值。 默认值是**adResyncAllValues**。  
  
## <a name="remarks"></a>备注  
  
## <a name="recordset"></a>记录集  
 使用**重新同步**方法来重新同步中当前的记录**记录集**与基础数据库。 如果使用静态或只进游标，但你想要查看基础数据库中的任何更改，这非常有用。  
  
 如果您设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**，**重新同步**功能仅适用于非只读**记录集**对象。  
  
 与不同[Requery](../../../ado/reference/ado-api/requery-method.md)方法，**重新同步**方法不会重新执行**记录集**对象的基本命令。 基础数据库中的新记录将不可见。  
  
 如果尝试重新同步失败由于与基础数据发生冲突 （例如，一条记录已被删除另一个用户），访问接口将返回到的警告[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合中，运行时错误时发生。 使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性 (**adFilterConflictingRecords**) 和[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性来查找有冲突的记录。  
  
 如果[唯一表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)并[Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)设置的动态属性，并**记录集**是执行多个表，则联接运算的结果**重新同步**方法将执行命令中给定**Resync Command**属性中命名的表上仅**唯一表**属性。  
  
## <a name="fields"></a>字段  
 使用**重新同步**方法来重新同步的值**字段**的集合**记录**具有基础数据源对象。 [计数](../../../ado/reference/ado-api/count-property-ado.md)属性不受此方法。  
  
 如果*ResyncValues*设置为**adResyncAllValues** （默认值）， [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)，[值](../../../ado/reference/ado-api/value-property-ado.md)，和[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)的属性[字段](../../../ado/reference/ado-api/field-object.md)同步集合中的对象。 如果*ResyncValues*设置为**adResyncUnderlyingValues**，将仅**UnderlyingValue**同步属性。  
  
 值**状态**属性为每个**字段**对象在调用时还会影响的行为**重新同步**。 有关**字段**具有对象**状态**的值**adFieldPendingUnknown**或者**adFieldPendingInsert**，**重新同步**不起作用。 有关**状态**的值**adFieldPendingChange**或**adFieldPendingDelete**，**重新同步**同步字段的数据值，数据源中仍存在。  
  
 **重新同步**将不会修改**状态**的值**域**对象，除非发生错误时**重新同步**调用。 例如，如果该字段不再存在，该提供程序将返回一个适当**状态**值**字段**对象，如**adFieldDoesNotExist**。 返回**状态**中的值可以以逻辑方式组合值**状态**属性。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [Resync 方法示例 (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Resync 方法示例 （VC + +）](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 属性](../../../ado/reference/ado-api/underlyingvalue-property.md)
