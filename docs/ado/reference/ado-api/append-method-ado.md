---
title: "Append 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9a192286d39660580968305d16cb159480b6a09a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-ado"></a>Append 方法 (ADO)
将对象追加到集合。 如果该集合为[字段](../../../ado/reference/ado-api/fields-collection-ado.md)，新[字段](../../../ado/reference/ado-api/field-object.md)追加到集合之前，可以创建对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parameters  
 *collection*  
 一个集合对象。  
  
 *fields*  
 A**字段**集合。  
  
 *对象*  
 对象变量表示要追加的对象。  
  
 *名称*  
 A**字符串**包含新的名称值**字段**对象，而且不能为相同的名称中的任何其他对象*字段*。  
  
 *类型*  
 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，其默认值为**adEmpty**，，指定新的字段的数据类型。 ADO，不支持以下数据类型和应不时使用追加到的新字段[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**， **adIUnknown**， **adVariant**。  
  
 *DefinedSize*  
 選擇性。 A**长**表示的定义的大小，以字符数或字节为单位的新字段的值。 此参数的默认值派生自*类型*。 具有的字段*DefinedSize*大于 255 个字节将被视为可变长度列。 默认值为*DefinedSize*未指定。  
  
 *Attrib*  
 選擇性。 A [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值，其默认值为**adFldDefault**，，指定新字段的特性。 如果未指定此值，该字段将包含派生自的特性*类型*。  
  
 *FieldValue*  
 選擇性。 A **Variant** ，表示新字段的值。 如果未指定，字段被追加一个 null 值。  
  
## <a name="remarks"></a>注释  
  
## <a name="parameters-collection"></a>Parameters 集合  
 必须设置[类型](../../../ado/reference/ado-api/type-property-ado.md)属性[参数](../../../ado/reference/ado-api/parameter-object.md)之前追加到的对象[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 如果你选择的可变长度数据类型，还必须设置[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)属性的值大于零。  
  
 描述参数自行最大程度减少到提供程序的调用，并因此可以提高性能，当你使用存储的过程或参数化的查询。 但是，你必须知道与存储过程或参数化你想要调用的查询的参数属性。  
  
 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法来创建**参数**相应的属性设置和使用的对象**追加**方法以将其添加到[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 这样就可以设置和返回参数值，而无需调用该提供程序的参数信息。 如果要写入的提供程序未提供参数信息，你必须使用此方法来手动填充**参数**为了根本使用参数的集合。  
  
## <a name="fields-collection"></a>字段集合  
 *FieldValue*添加时，参数才有效**字段**对象传递给[记录](../../../ado/reference/ado-api/record-object-ado.md)对象，不适用于**记录集**对象。 与**记录**对象，可以将字段追加，还可以在同一时间提供值。 与**记录集**对象，你必须创建时的字段**记录集**并已关闭，然后打开**记录集**并将值分配给字段。  
  
> [!NOTE]
>  新**字段**已追加到的对象**字段**集合**记录**对象，[值](../../../ado/reference/ado-api/value-property-ado.md)属性必须设置在任何其他之前**字段**可以指定属性。 首先，为特定值**值**属性必须具有已分配和[更新](../../../ado/reference/ado-api/update-method.md)上**字段**名集合。 然后，其他属性，如[类型](../../../ado/reference/ado-api/type-property-ado.md)或[属性](../../../ado/reference/ado-api/attributes-property-ado.md)可访问。 **字段**以下数据类型的对象 (**DataTypeEnum**) 无法附加到**字段**集合并将会导致发生错误： **adArray**， **adChapter**， **adEmpty**， **adPropVariant**，和**adUserDefined**。 此外，以下数据类型不受 ADO: **adIDispatch**， **adIUnknown**，和**adIVariant**。 对于这些类型，不会发生错误时追加，但使用时会产生不可预知的结果，包括内存泄漏。  
  
## <a name="recordset"></a>记录集  
 如果你未设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性之前调用**追加**方法， **CursorLocation**将设置为**adUseClient** ([CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值) 时自动[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)调用对象。  
  
 如果将发生运行时错误**追加**方法调用**字段**集合打开**记录集**，或在**记录集**其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)设置属性。 你可以仅将附加到的字段**记录集**未处于打开状态，尚未连接到数据源。 这通常是这种情况时**记录集**对象制造与[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法或分配给变量的对象。  
  
## <a name="record"></a>記錄  
 如果将不会发生运行时错误**追加**方法调用**字段**集合打开**记录**。 新的字段将添加到**字段**集合**记录**对象。 如果**记录**派生自**记录集**，新的字段不会出现在**字段**集合**记录集**对象。  
  
 可以创建一个非存在的字段，并将其追加到**字段**通过将值分配给字段对象，就像它已存在于集合中的集合。 赋值将触发的自动创建并追加的**字段**对象，然后分配将会完成。  
  
 后追加**字段**到**字段**集合**记录**对象，请调用**更新**方法**字段**集合以保存更改。  
  
## <a name="applies-to"></a>适用范围  
  
- [字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [参数集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [追加和 CreateParameter 方法示例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [追加和 CreateParameter 方法示例 （VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 方法 （ADO 字段集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 参数集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
