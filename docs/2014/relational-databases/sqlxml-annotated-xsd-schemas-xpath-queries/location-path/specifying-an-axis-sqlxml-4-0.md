---
title: 指定轴 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f3b9f58369cea876bc345300a945f85260b4326a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018153"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定轴 (SQLXML 4.0)
    
-   轴指定根据位置步骤和上下文节点选择的节点之间的树关系。 支持以下轴：`child`  
  
     包含上下文节点的子级。  
  
     下面的 XPath 表达式 （位置路径） 选择从当前上下文节点所有**\<客户 >** 子级：  
  
    ```  
    child::Customer  
    ```  
  
     在下面的 XPath 查询中，`child` 为轴。 `Customer` 是节点测试。  
  
-   `parent`  
  
     包含上下文节点的父级。  
  
     下面的 XPath 表达式选择所有**\<客户 >** 的父级**\<顺序 >** 子级：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     这与指定 `child::Customer` 的作用相同。 在此 XPath 查询中，`child` 和 `parent` 为轴。 `Customer` 和 `Order` 是节点测试。  
  
-   `attribute`  
  
     包含上下文节点的属性。  
  
     下面的 XPath 表达式选择**CustomerID**的上下文节点的属性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     包含上下文节点本身。  
  
     下面的 XPath 表达式选择当前节点是否**\<顺序 >** 节点：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查询中，`self` 为轴，`Order` 为节点测试。  
  
  