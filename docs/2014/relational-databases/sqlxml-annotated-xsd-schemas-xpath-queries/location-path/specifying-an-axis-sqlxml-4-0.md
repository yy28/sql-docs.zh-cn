---
title: 指定轴（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: rothja
ms.author: jroth
ms.openlocfilehash: 651b7899e104fe5a7dbc6d584ceba6e5cf8de570
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055118"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定轴 (SQLXML 4.0)
    
-   轴指定根据位置步骤和上下文节点选择的节点之间的树关系。 支持以下轴：`child`  
  
     包含上下文节点的子级。  
  
     以下 XPath 表达式（位置路径）从当前上下文节点选择所有 **\<Customer>** 子级：  
  
    ```  
    child::Customer  
    ```  
  
     在下面的 XPath 查询中，`child` 为轴。 `Customer` 是节点测试。  
  
-   `parent`  
  
     包含上下文节点的父级。  
  
     下面的 XPath 表达式选择子级的所有 **\<Customer>** 父级 **\<Order>** ：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     这与指定 `child::Customer` 的作用相同。 在此 XPath 查询中，`child` 和 `parent` 为轴。 `Customer` 和 `Order` 是节点测试。  
  
-   `attribute`  
  
     包含上下文节点的属性。  
  
     下面的 XPath 表达式选择上下文节点的**CustomerID**属性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     包含上下文节点本身。  
  
     下面的 XPath 表达式选择当前节点（如果它是 **\<Order>** 节点）：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查询中，`self` 为轴，`Order` 为节点测试。  
  
  
