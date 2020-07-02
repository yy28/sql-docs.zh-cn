---
title: 指定轴（SQLXML）
description: 了解如何在 SQLXML 4.0 XPath 查询中指定轴指定 location 步骤所选的节点与上下文节点之间的关系。
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df40d531bcb9c1fddcad5d78cd76ca98831834ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85649731"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定轴 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
    
-   轴指定根据位置步骤和上下文节点选择的节点之间的树关系。 支持以下轴： **child**  
  
     包含上下文节点的子级。  
  
     以下 XPath 表达式（位置路径）从当前上下文节点选择所有 **\<Customer>** 子级：  
  
    ```  
    child::Customer  
    ```  
  
     在下面的 XPath 查询中，`child` 为轴。 `Customer` 是节点测试。  
  
-   **上层**  
  
     包含上下文节点的父级。  
  
     下面的 XPath 表达式选择子级的所有 **\<Customer>** 父级 **\<Order>** ：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     这与指定 `child::Customer` 的作用相同。 在此 XPath 查询中，`child` 和 `parent` 为轴。 `Customer` 和 `Order` 是节点测试。  
  
-   **attribute**  
  
     包含上下文节点的属性。  
  
     下面的 XPath 表达式选择上下文节点的**CustomerID**属性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **解压**  
  
     包含上下文节点本身。  
  
     下面的 XPath 表达式选择当前节点（如果它是 **\<Order>** 节点）：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查询中，`self` 为轴，`Order` 为节点测试。  
  
  
