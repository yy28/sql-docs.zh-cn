---
title: "重新调整 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5264de973e4ed36cc24eb5c535576bdfa0a7228
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="reshaping"></a>重新调整
A**记录集**创建可能的形状的子句来指定命令*别名*名称 （通常使用 AS 关键字）。 形状的别名**记录集**可以完全不同的命令中引用。 也就是说，你可以重复使用，或*重塑*，以前整形**记录集**新形状命令中。 若要支持此功能，ADO 提供一个属性，[重新调整形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 重新调整有两个主要功能。 第一种是将相关联的现有**记录集**使用新的父**记录集**。  
  
## <a name="example"></a>示例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二个函数是，启用到现有子非章节访问**记录集**对象，使用语法"形状\<记录集重新调整形状名称 >"。  
  
> [!NOTE]
>  不能将列追加到现有**记录集**，重新调整形状参数化**记录集**或**记录集**对象在任何干预计算子句中，或执行聚合操作任何**记录集**子代从**记录集**改变了形状的。 **记录集**改变了形状的和新形状命令都必须使用相同[连接](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>另请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)

