---
title: 数据定形示例 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0685e0c593a77f5369513fa9b39fe61f89498ff4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="data-shaping-example"></a>调整示例数据
以下数据调整命令演示如何生成分层结构**记录集**从**客户**和**订单**Northwind 数据库中的表。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 当使用此命令以打开**记录集**对象 (中所示[Visual Basic 示例的数据调整](../../../ado/guide/data/visual-basic-example-of-data-shaping.md))，它将创建一个章节 (**chapOrders**) 为返回每个记录从**客户**表。 本章包含的子集**记录集**从返回**订单**表。 **ChapOrders**章包含有关给定客户的订单的所有请求的信息。 在此示例中，章包含三列： **OrderID**， **OrderDate**，和**CustomerID**。  
  
 调整所产生的前两个条目**记录集**如下所示：  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 在形状命令中，追加用于创建子级**记录集**与父**记录集**（如所讨论在形状关键字后立即从提供程序特定命令返回更早版本） 通过 RELATE 子句。 父级和子级通常都有至少一个列共同点： 的父行中的列的值是在所有的子行中列的值相同。  
  
 没有使用形状命令第二种方法： 即，若要生成父**记录集**从子**记录集**。 子组织单位中的记录**记录集**进行分组，通常通过使用了 BY 子句中和一个行添加到父**记录集**子组织单位中每个生成组。 如果省略了 BY 子句，则子**记录集**单个组和父级，则将窗体**记录集**将包含恰好一个行。 这可用于通过整个子计算"总计"聚合**记录集**。  
  
 形状命令构造还允许你以编程方式创建特定形状**记录集**。 然后，就可以访问的组件**记录集**以编程方式或通过适当的可视化控件。 发出了形状命令会像任何其他 ADO 命令文本。 有关详细信息，请参阅[形状的命令通常](../../../ado/guide/data/shape-commands-in-general.md)。  
  
 无论采用哪种方式父**记录集**是格式正确，它将包含用于与子级的章节列**记录集**。 如果你想，父**记录集**还可以通过子行具有包含聚合 （SUM、 MIN、 MAX 和等等） 的列。 父级和子级**记录集**可以包含在中的行的表达式中的列**记录集**，以及列的新和最初为空。  
  
 本部分将继续与以下主题。  
  
-   [Visual Basic 数据整理示例](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
