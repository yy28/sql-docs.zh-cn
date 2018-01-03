---
title: "AddNew 方法 (ADO) |Microsoft 文档"
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
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords: AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 51978e39a34b02238d4c0b1658620c9ba8d538a6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="addnew-method-ado"></a>AddNew 方法 (ADO)
创建可更新的新记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parameters  
 *记录集*  
 A**记录集**对象。  
  
 *字段列表*  
 可选。 单个名称或名称的数组或新记录中的字段的序号位置。  
  
 *值*  
 可选。 单个值，则新记录中字段的值为数组。 如果*Fieldlist*是一个数组，*值*必须也为数组具有相同成员的数目; 否则为将会出错。 字段名称的顺序必须匹配每个数组中的字段值的顺序。  
  
## <a name="remarks"></a>Remarks  
 使用**AddNew**方法创建并初始化一个新的记录。 使用[支持](../../../ado/reference/ado-api/supports-method.md)方法替换**adAddNew** ( [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)值) 以验证是否可以将记录添加到当前**记录集**对象。  
  
 调用后**AddNew**方法，新的记录将成为当前记录和调用方法后仍当前[更新](../../../ado/reference/ado-api/update-method.md)方法。 由于新的记录追加到**记录集**，调用**MoveNext**更新后的末尾将移动**记录集**，这会让**EOF** True。 如果**记录集**对象不支持书签，你可能无法访问新的记录，一旦您移动到另一条记录。 具体取决于游标类型，你可能需要调用[Requery](../../../ado/reference/ado-api/requery-method.md)方法，以便可以访问新的记录。  
  
 如果调用**AddNew** ADO 时编辑当前记录或添加新记录时，调用**更新**方法来保存任何更改，然后创建新的记录。  
  
 行为**AddNew**方法取决于的更新模式**记录集**对象和是否传递*Fieldlist*和*值*自变量。  
  
 在*立即更新模式*(在其中提供程序将更改写入基础数据源一旦调用**更新**方法)，则调用**AddNew**不带方法自变量集[EditMode](../../../ado/reference/ado-api/editmode-property.md)属性**adEditAdd** ( [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值)。 提供程序将任何字段值更改在本地缓存。 调用**更新**方法发送到数据库的新记录，并将重置**EditMode**属性**adEditNone** ( **EditModeEnum**值)。 如果你通过*Fieldlist*和*值*自变量，ADO 立即发送到数据库的新记录 (没有**更新**调用是必需的); **EditMode**属性值不会更改 (**adEditNone**)。  
  
 在*批处理更新模式下*(在其中提供程序缓存多个更改，并将其写入到基础数据源仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，则调用**AddNew**方法，而自变量集**EditMode**属性**adEditAdd**。 提供程序将任何字段值更改在本地缓存。 调用**更新**方法将新的记录添加到当前**记录集**，但提供程序不将更改发布到基础数据库中，或重置**EditMode**到**adEditNone**，直到你调用**UpdateBatch**方法。 如果你通过*Fieldlist*和*值*自变量，则 ADO 会将新记录发送到的提供程序集缓存中存储**EditMode**到**adEditAdd**; 你需要调用**UpdateBatch**方法发布到基础数据库的新记录。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用字段列表和包含，若要了解如何为数组中包括的字段列表和值列表的值列表的 AddNew 方法。  
  
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
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [AddNew 方法示例 (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew 方法示例 (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [AddNew 方法示例 （VC + +）](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [正在执行方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 属性](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [支持方法](../../../ado/reference/ado-api/supports-method.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
