---
title: 数据整理示例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92e34de1b9fd675570527f9a28f8476a51597f10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472554"
---
# <a name="data-shaping-example"></a>数据整理示例
以下数据整理命令演示了如何构建一种分层**记录集**从**客户**并**订单**Northwind 数据库中的表。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 当使用此命令以打开**记录集**对象 (如中所示[Visual Basic 示例的数据整理](../../../ado/guide/data/visual-basic-example-of-data-shaping.md))，它会创建一个章节 (**chapOrders**) 返回每个记录从**客户**表。 本章包含的子集**记录集**返回从**订单**表。 **ChapOrders**章包含有关所发出的给定客户订单的所有请求的信息。 在此示例中，一章包含三列：**OrderID**， **OrderDate**，和**CustomerID**。  
  
 所产生的形状的前两个条目**记录集**如下所示：  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 在形状命令中，追加用于创建子级**记录集**与父**记录集**（因为特定于提供程序的命令已讨论的形状关键字后立即返回早） 通过 RELATE 子句。 父级和子级通常共同具有至少一列：中的父行的列的值为子级的所有行中的列的值相同。  
  
 没有使用形状命令的第二个方法： 即生成一个父级**记录集**来自子元素**记录集**。 子组织单位中的记录**记录集**进行分组，通常使用 BY 子句和一个行添加到父**记录集**子组织单位中每个生成组。 如果省略了 BY 子句，则子**记录集**单个组和父级将窗体**记录集**将包含一个行。 这可用于对整个子计算"总计"聚合**记录集**。  
  
 形状命令构造还可以以编程方式创建形状**记录集**。 然后，您可以访问的组件**记录集**以编程方式或通过相应的可视化控件。 形状命令发出类似于任何其他 ADO 命令文本。 有关详细信息，请参阅[形状的命令通常](../../../ado/guide/data/shape-commands-in-general.md)。  
  
 无论采用哪种方式父级**记录集**是格式正确，它将包含用于相关的一个子级的章节列**记录集**。 如果你想，父级**记录集**还可以包含聚合 （SUM、 MIN、 MAX 等） 的列的子行。 父级和子级**记录集**可以有包含在中的行的表达式中的列**记录集**，以及列即新建和最初为空。  
  
 本部分继续执行下面的主题。  
  
-   [Visual Basic 数据整理示例](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
