---
title: 改变 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 213ed5f05133733b8336f184599ca8ef3e4028a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924355"
---
# <a name="reshaping"></a>重新整理
可以为 shape 命令的子句创建的**记录集**指定*别名*（通常使用 AS 关键字）。 可以在完全不同的命令中引用成形**记录集**的别名。 也就是说，您可以在新的 shape 命令中重复使用或*改变*先前形状的**记录集**。 为了支持此功能，ADO 提供了一个属性，该属性[调整了名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 重构有两个主要功能。 第一种方式是将现有**记录集**与新的父**记录集**相关联。  
  
## <a name="example"></a>示例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二个函数是启用对现有子**记录集**对象的非章节访问，并使用语法 " \<形状记录集重新整形名称>"。  
  
> [!NOTE]
>  不能将列追加到现有**记录集**、改变参数化**记录集**或任何干预计算子句中的**记录集**对象的列，或者对要调整的**记录集中**的任何**记录集**后代执行聚合运算。 要调整的**记录集**和新的 shape 命令必须都使用相同的[连接](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)
