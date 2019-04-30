---
title: 重塑 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 324801cbfc97db4e2a1137fa04df0c74dc1897a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280397"
---
# <a name="reshaping"></a>重新整理
一个**记录集**创建形状的子句命令可能会分配*别名*名称 （通常使用 AS 关键字）。 形状的别名**记录集**可以完全不同的命令中引用。 也就是说，您可以重复使用，或*重塑*，以前形状**记录集**中新的形状命令。 若要支持此功能，ADO，提供了一个属性，[改变形状名称](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 重新调整具有两个主要功能。 第一种是将相关联的现有**记录集**使用新的父**记录集**。  
  
## <a name="example"></a>示例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二个函数是用于非章节访问现有的子**记录集**对象，使用语法"形状\<记录集重新调整形状名称 >"。  
  
> [!NOTE]
>  不能将列追加到现有**记录集**，调整参数化**记录集**或**记录集**任何干预的 COMPUTE 子句中的对象或执行聚合对任何的操作**记录集**的后代**记录集**改变了形状的。 **记录集**改变了形状的和新形状命令都必须使用相同[连接](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)
