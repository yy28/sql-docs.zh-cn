---
title: Optimize 属性-动态 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e8bb3c3787effe8418db735a72425a793b73e35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931855"
---
# <a name="optimize-property-dynamic-ado"></a>Optimize 属性 - 动态 (ADO)
指定是否应在创建索引[字段](../../../ado/reference/ado-api/field-object.md)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**布尔**值，该值指示是否应创建索引。  
  
## <a name="remarks"></a>备注  
 索引可以提高查找或中的值进行排序的操作的性能[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 索引是内部的 ADO;无法显式访问或应用程序中使用。  
  
 若要在字段上创建索引，请设置**优化**属性设置为**True**。 若要删除索引，请将此属性设置为**False**。  
  
 **优化**动态属性追加到[字段](../../../ado/reference/ado-api/field-object.md)对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="usage"></a>用法  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>适用范围  
 [字段对象](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>请参阅  
 [Optimize 属性示例 (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Optimize 属性示例 （VC + +）](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [筛选器属性](../../../ado/reference/ado-api/filter-property.md)   
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort 属性](../../../ado/reference/ado-api/sort-property.md)
