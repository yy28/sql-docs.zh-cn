---
title: 排序属性 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 692a6a3e9ca2e65b031aebd8ed99c2719f0f0a69
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sort-property"></a>排序属性
指示在其上的一个或多个字段名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)进行排序，并且每个字段是否以升序或降序进行排序。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**中的值，该值指示字段名称**记录集**排序依据。 每个名称使用逗号分隔，并且 （可选） 可以后跟空白和关键字， **ASC**，其中进行排序以升序，字段或**DESC**，这对按降序字段进行排序。 默认情况下，如果未指定关键字，该字段是以升序排序。  
  
## <a name="remarks"></a>注释  
 此属性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 对于每个字段中指定将创建一个临时索引**排序**如果索引不存在的属性。  
  
 排序操作是高效的因为数据不以物理方式重新排列，但只由索引指定的顺序进行访问。  
  
 时的值**排序**属性是空字符串，之外的任何**排序**属性顺序将优先于中指定的顺序**ORDER BY**子句用来打开的 SQL 语句中包含**记录集**。  
  
 **记录集**不必在访问前打开**排序**属性; 它可以在后随时设置**记录集**实例化对象。  
  
 设置**排序**属性为空字符串将行重置为其原始顺序并删除临时索引。 将删除现有索引。  
  
 假设**记录集**包含名为的三个字段*firstName*，*没为*，和*lastName*。 设置**排序**到字符串，属性"`lastName DESC, firstName ASC`"，顺序将**记录集**按姓氏以降序排序，然后按名字以升序。 中间名首字母将被忽略。  
  
 没有字段可以命名为"ASC"或"DESC"，因为这些名称与关键字冲突**ASC**和**DESC**。 你可以通过创建名称有冲突的字段别名**AS**返回的查询中的关键字**记录集**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [排序属性示例 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [排序属性示例 （VC + +）](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [优化属性的动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 属性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
