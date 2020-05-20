---
title: AddNew 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: rothja
ms.author: jroth
ms.openlocfilehash: a6359d1b9f69963120e9446c47aa5473beedd127
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760723"
---
# <a name="addnew-method-ado"></a>AddNew 方法 (ADO)
为可更新的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象创建新记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>参数  
 *记录集*  
 **记录集**对象。  
  
 *FieldList*  
 可选。 单个名称，或者新记录中字段的名称或序号位置的数组。  
  
 *值*  
 可选。 单个值，或新记录中的字段的值数组。 如果*Fieldlist*是一个数组，则*值*也必须是具有相同成员数的数组;否则，将发生错误。 字段名称的顺序必须与每个数组中的字段值顺序相匹配。  
  
## <a name="remarks"></a>备注  
 使用**AddNew**方法创建并初始化新记录。 使用 with **adAddNew** （ [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)值）的[支持](../../../ado/reference/ado-api/supports-method.md)方法验证是否可以将记录添加到当前**记录集**对象。  
  
 调用**AddNew**方法之后，新记录将成为当前记录，并在调用[Update](../../../ado/reference/ado-api/update-method.md)方法后保持最新。 由于新记录将追加到**记录集中**，因此 **，对更新**进行的调用将移过**记录集**的末尾，使**EOF**为 True。 如果**记录集**对象不支持书签，则在移动到另一记录后，您可能无法访问新记录。 根据游标类型，可能需要调用[Requery](../../../ado/reference/ado-api/requery-method.md)方法以使新记录可访问。  
  
 如果在编辑当前记录或添加新记录时调用**AddNew** ，ADO 将调用**Update**方法来保存所有更改，然后创建新记录。  
  
 **AddNew**方法的行为取决于**记录集**对象的更新模式，以及是否传递*Fieldlist*和*Values*参数。  
  
 在*即时更新模式下*（在调用**update**方法后，提供程序将更改写入基础数据源），调用不带参数的**AddNew**方法会将[EditMode](../../../ado/reference/ado-api/editmode-property.md)属性设置为**adEditAdd** （ [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值）。 提供程序在本地缓存任何字段值更改。 调用**Update**方法会将新记录发送到数据库，并将**EditMode**属性重置为**adEditNone** （ **EditModeEnum**值）。 如果传递*Fieldlist*和*VALUES*参数，ADO 会立即将新记录发送到数据库（无需**更新**调用）;**EditMode**属性值不会更改（**adEditNone**）。  
  
 在*批处理更新模式下*（其中，提供程序缓存多个更改并仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法时将它们写入基础数据源），调用不带参数的**AddNew**方法会将**EditMode**属性设置为**adEditAdd**。 提供程序在本地缓存任何字段值更改。 调用**Update**方法会将新记录添加到当前**记录集**，但访问接口不会将更改发布到基础数据库中，也不会将**EditMode**重置为**adEditNone**，直到调用**UpdateBatch**方法。 如果传递*Fieldlist*和*VALUES*参数，ADO 会将新记录发送到缓存中的存储提供程序，并将**EditMode**设置为**adEditAdd**;需要调用**UpdateBatch**方法将新记录发布到基础数据库。  
  
## <a name="example"></a>示例  
 下面的示例演示如何对包含的字段列表和值列表使用 AddNew 方法，以了解如何将字段列表和值列表作为数组包含在内。  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AddNew 方法示例（VB）](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew 方法示例（VBScript）](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [AddNew 方法示例（VC + +）](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [支持方法](../../../ado/reference/ado-api/supports-method.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
