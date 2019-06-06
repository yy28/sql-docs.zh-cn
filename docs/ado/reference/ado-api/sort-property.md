---
title: 对属性进行排序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 092eb49216874a59e4bcba09431fcc01dc3679a4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711161"
---
# <a name="sort-property"></a>Sort 属性
指示在其上的一个或多个字段名称[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)进行排序和每个字段按升序或降序顺序排序。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回**字符串**中的值，该值指示该字段名称**记录集**作为排序依据。 每个名称是用逗号分隔的并可以选择后跟一个空格和关键字， **ASC**，其中进行排序的字段按升序排列，或**DESC**，这对字段按降序进行排序。 默认情况下，如果不指定任何关键字，则该字段按升序顺序。  
  
## <a name="remarks"></a>备注  
 此属性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 对于每个字段中指定将创建一个临时索引**排序**如果索引不存在的属性。  
  
 排序操作是有效的因为数据不以物理方式重新排列，但只由索引指定的顺序进行访问。  
  
 时的值**排序**属性是空字符串，之外的任何**排序**属性顺序的优先级高于中指定的顺序**ORDER BY**子句用于打开 SQL 语句中包括**记录集**。  
  
 **记录集**无需访问之前打开**排序**属性; 它可以在任何时间后设置**记录集**实例化对象。  
  
 设置**排序**属性为空字符串将行重置为其原始顺序并删除临时索引。 将删除现有的索引。  
  
 假设**记录集**包含名为三个字段*firstName*， *middleInitial*，以及*lastName*。 设置**排序**属性设置为字符串，"`lastName DESC, firstName ASC`"，将顺序**记录集**按姓氏以降序排序，然后按升序排序的第一个名称。 中间名首字母将被忽略。  
  
 无字段可命名为"ASC"或"DESC"因为这些名称与关键字冲突**ASC**并**DESC**。 通过创建具有冲突名称的字段的别名**AS**中返回的查询关键字**记录集**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Sort 属性示例 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort 属性示例 （VC + +）](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize 属性-动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 属性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 属性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
