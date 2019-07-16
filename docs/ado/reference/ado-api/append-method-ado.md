---
title: Append 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 17fa0ff30e8dcdbf7ea67080f17c3e066bba8605
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920675"
---
# <a name="append-method-ado"></a>Append 方法 (ADO)
将对象追加到集合。 如果集合是[字段](../../../ado/reference/ado-api/fields-collection-ado.md)，一个新[字段](../../../ado/reference/ado-api/field-object.md)之前将其追加到集合，可创建对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parameters  
 *collection*  
 集合对象。  
  
 *字段*  
 一个**字段**集合。  
  
 *object*  
 一个表示要追加的对象的对象变量。  
  
 *名称*  
 一个**字符串**值，该值包含新名称**字段**对象，并不能相同的名称中的任何其他对象*字段*。  
  
 *类型*  
 一个[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，其默认值为**adEmpty**，指定新字段的数据类型。 ADO 中，不支持以下数据类型和应不时，使用追加到新的字段[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**， **adIUnknown**， **adVariant**。  
  
 *DefinedSize*  
 可选。 一个**长**值，该值表示定义的大小，以字节为单位的新字段或字符。 此参数的默认值派生自*类型*。 具有字段*DefinedSize*大于 255 个字节将被视为可变长度列。 默认值为*DefinedSize*未指定。  
  
 *Attrib*  
 可选。 一个[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值，其默认值为**adFldDefault**，，指定新字段的特性。 如果未指定此值，该字段将包含属性派生自*类型*。  
  
 *FieldValue*  
 可选。 一个**变体**，表示新字段的值。 如果未指定，该字段追加值为 null。  
  
## <a name="remarks"></a>备注  
  
## <a name="parameters-collection"></a>Parameters 集合  
 必须设置[类型](../../../ado/reference/ado-api/type-property-ado.md)的属性[参数](../../../ado/reference/ado-api/parameter-object.md)之前追加到对象[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 如果选择可变长度数据类型，则还必须设置[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)属性设置为大于零的值。  
  
 自己描述参数最大程度减少对提供程序的调用，因此可以提高性能，使用存储的过程或参数化的查询时。 但是，您必须知道的参数的属性关联的存储过程或参数化您想要调用的查询。  
  
 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法来创建**参数**具有相应的属性设置和使用的对象**追加**方法将其添加到[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 这样可以设置和返回参数值，而无需调用的参数信息的提供程序。 如果你正在编写不提供参数信息的提供程序，必须使用此方法来手动填充**参数**集合，以便在所有使用参数。  
  
## <a name="fields-collection"></a>字段集合  
 *FieldValue*添加时，参数才有效**字段**对象传递给[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，不**记录集**对象。 与**记录**对象，可以将附加字段，并在同一时间提供值。 与**记录集**对象，您必须创建字段时**记录集**已关闭，，然后打开**记录集**并将值分配到的字段。  
  
> [!NOTE]
>  对新**字段**已追加到的对象**字段**的集合**记录**对象，[值](../../../ado/reference/ado-api/value-property-ado.md)属性必须设置在任何其他前**字段**可以指定属性。 首先，为特定值**值**属性必须具有已分配和[更新](../../../ado/reference/ado-api/update-method.md)上**字段**名集合。 然后，其他属性，如[类型](../../../ado/reference/ado-api/type-property-ado.md)或[属性](../../../ado/reference/ado-api/attributes-property-ado.md)可访问。 **字段**以下数据类型的对象 (**DataTypeEnum**) 不能追加到**字段**集合，并将导致出现错误： **adArray**，**adChapter**， **adEmpty**， **adPropVariant**，以及**adUserDefined**。 此外，通过 ADO 不支持以下数据类型： **adIDispatch**， **adIUnknown**，并**adIVariant**。 对于这些类型，不会发生错误时追加，但使用时会产生不可预知的结果，包括内存泄漏。  
  
## <a name="recordset"></a>记录集  
 如果未设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性，然后再调用**追加**方法， **CursorLocation**将被设置为**adUseClient** ([CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值) 时自动[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)调用对象。  
  
 如果将发生运行时错误**追加**上调用方法**字段**的一种开放集合**记录集**，或在**记录集**其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)设置属性。 仅可以将附加到的字段**记录集**的未打开，并且尚未连接到数据源。 这通常是这种情况时**记录集**对象会生成与[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法或分配给对象变量。  
  
## <a name="record"></a>录制  
 如果将不会发生运行时错误**追加**上调用方法**字段**的一种开放集合**记录**。 该新字段将添加到**字段**系列**记录**对象。 如果**记录**派生自**记录集**，新字段不会出现在**字段**系列**记录集**对象。  
  
 可以创建一个不存在的字段，并将其追加到**字段**通过将值分配给字段对象，如同它已存在于集合中的集合。 赋值将触发自动创建和追加**字段**对象，然后分配将被完成。  
  
 后追加**字段**到**字段**的集合**记录**对象，请调用**更新**方法**字段**集合以保存更改。  
  
## <a name="applies-to"></a>适用范围  
  
- [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Append 和 CreateParameter 方法示例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append 和 CreateParameter 方法示例 （VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
