---
title: 更新方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae2645057670ba65a33bb8b5da238c7e01790ae9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713785"
---
# <a name="update-method"></a>Update 方法
将保存到的当前行的任何更改[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parameters  
 *Fields*  
 可选。 一个**Variant** ，表示单个名称或**变体**数组，它表示名称或序号位置或多个你想要修改的字段。  
  
 *值*  
 可选。 一个**Variant** ，表示单个值，或**变体**数组，它表示字段或新记录中的字段的值。  
  
## <a name="remarks"></a>备注  
  
## <a name="recordset"></a>记录集  
 使用**更新**方法保存的当前记录的任何更改**记录集**对象调用以来[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法或以来更改中的任何字段值现有记录。 **记录集**对象必须支持更新。  
  
 若要设置字段值，请执行以下操作：  
  
-   将值分配给[字段](../../../ado/reference/ado-api/field-object.md)对象的[值](../../../ado/reference/ado-api/value-property-ado.md)属性并调用**更新**方法。  
  
-   将字段名称和值作为参数传递**更新**调用。  
  
-   将字段名称的数组和数组值传递**更新**调用。  
  
 当您使用的字段和值的数组时，必须有相同数目的两个数组中的元素。 此外，字段名称的顺序必须与匹配的字段值的顺序。 如果不匹配的数量和顺序的字段和值，就会出错。  
  
 如果**记录集**对象支持批量更新，你可以本地直到你调用缓存到一个或多个记录的多个更改[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 如果正在编辑当前记录或添加新记录，在调用时**UpdateBatch**方法，将自动调用 ADO**更新**方法将任何挂起的更改保存到之前的当前记录传输批的更改为提供程序。  
  
 如果将从该记录移正在添加或编辑，然后再调**更新**方法，将自动调用 ADO**更新**以保存所做的更改。 必须调用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法如果你想要取消对当前记录所做的任何更改或放弃新添加的记录。  
  
 当前记录保持最新调用后**更新**方法。  
  
## <a name="record"></a>录制  
 **更新**方法完成添加、 删除和更新中的字段[字段](../../../ado/reference/ado-api/fields-collection-ado.md)的集合**记录**对象。  
  
 例如，使用删除的字段**删除**方法将立即标记为待删除，但保留在集合中。 **更新**必须调用方法来从提供程序的集合中实际删除这些字段。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [Update 和 CancelUpdate 方法示例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法示例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
