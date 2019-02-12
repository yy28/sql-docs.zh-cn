---
title: 指定轴 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5f35aaa9009d07e4dad6f7c5309d9f2bb6c23ea4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013318"
---
# <a name="specifying-an-axis-sqlxml-40"></a>指定轴 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   轴指定根据位置步骤和上下文节点选择的节点之间的树关系。 支持以下轴：**子**  
  
     包含上下文节点的子级。  
  
     以下 XPath 表达式 （位置路径） 从所有当前上下文节点选择**\<客户 >** 子级：  
  
    ```  
    child::Customer  
    ```  
  
     在下面的 XPath 查询中，`child` 为轴。 `Customer` 是节点测试。  
  
-   **parent**  
  
     包含上下文节点的父级。  
  
     下面的 XPath 表达式选择所有**\<客户 >** 的父级**\<顺序 >** 子级：  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     这与指定 `child::Customer` 的作用相同。 在此 XPath 查询中，`child` 和 `parent` 为轴。 `Customer` 和 `Order` 是节点测试。  
  
-   **attribute**  
  
     包含上下文节点的属性。  
  
     以下 XPath 表达式选择**CustomerID**上下文节点的属性：  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **self**  
  
     包含上下文节点本身。  
  
     下面的 XPath 表达式选择当前节点，如果它是**\<顺序 >** 节点：  
  
    ```  
    self::Order  
    ```  
  
     在此 XPath 查询中，`self` 为轴，`Order` 为节点测试。  
  
  
