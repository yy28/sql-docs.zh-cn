---
title: "更新方法 |Microsoft 文档"
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
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 287fb5bf8b87a8371ee84d89ba4e5efee6b3587f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="update-method"></a>Update 方法
将保存的当前行的任何更改[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parameters  
 *字段*  
 可选。 A **Variant**表示单个名称或**Variant**数组，表示名称或序号位置或多个你想要修改的字段。  
  
 *值*  
 可选。 A **Variant**表示单个值，或**Variant**数组，表示字段或新记录中的字段的值。  
  
## <a name="remarks"></a>注释  
  
## <a name="recordset"></a>记录集  
 使用**更新**方法以将保存的当前记录的任何更改**记录集**以来调用的对象[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法或以来更改中的任何字段值现有记录。 **记录集**对象必须支持更新。  
  
 若要设置字段值，请执行以下操作：  
  
-   将值分配给[字段](../../../ado/reference/ado-api/field-object.md)对象的[值](../../../ado/reference/ado-api/value-property-ado.md)属性并调用**更新**方法。  
  
-   将字段名称和值作为参数传递**更新**调用。  
  
-   将字段名称的数组和数组值与传递**更新**调用。  
  
 当你使用的字段和值的数组时，必须有两个数组中元素的数量相等。 此外，字段名称的顺序必须匹配字段值的顺序。 如果不匹配的数量和顺序的字段和值，就会出错。  
  
 如果**记录集**对象支持批处理更新，你可以本地直到你调用缓存到一个或多个记录的多个更改[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 如果你要编辑的当前记录或添加一条新记录，当你调用**UpdateBatch**方法时，将自动调用 ADO**更新**方法将任何挂起的更改保存到之前的当前记录传输到提供程序的批处理的更改。  
  
 如果你将从该记录移正在添加或编辑，然后再调**更新**方法时，将自动调用 ADO**更新**以保存所做的更改。 必须调用[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法如果你想要取消对当前记录所做的任何更改或丢弃新添加的记录。  
  
 当前记录后，仍当前调用**更新**方法。  
  
## <a name="record"></a>录制  
 **更新**方法完成添加、 删除和中的字段的更新[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合**记录**对象。  
  
 例如，字段随删除**删除**方法将立即标记为删除，但保留在集合中。 **更新**必须调用方法来从提供程序的集合中实际删除这些字段。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [更新和正在执行的方法示例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [更新和正在执行的方法示例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [正在执行方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)

