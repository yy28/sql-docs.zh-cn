---
title: 在位置路径中指定节点测试（SQLXML）
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f94f155ee86df6daf0c039a18f27c30e294d57df
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254741"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路径中指定节点测试 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  节点测试指定根据位置步骤选择的节点类型。 每个轴（**子级**、 **parent**、 **attribute**或**self**）都具有一个主体节点类型。 对于**属性**轴，主体节点类型为** \<attribute>**。 对于**parent**、 **child**和**self**轴，主体节点类型为** \<元素>**。  
  
> [!NOTE]  
>  不支持通配符节点测试 *（例如 `child::*`）。  
  
## <a name="node-test-example-1"></a>节点测试：示例1  
 位置路径`child::Customer`选择** \<** 上下文节点的 Customer>元素子级。  
  
 在本示例中，`child` 是轴，`Customer` 是节点测试。 **子**轴的主体节点类型为** \<元素>**。 因此，如果** \<Customer>** 节点是>节点的** \<元素**，则节点测试为 TRUE。 如果上下文节点没有** \<客户>** 子级，则返回一组空节点。  
  
## <a name="node-test-example-2"></a>节点测试：示例 2  
 位置路径`attribute::CustomerID`选择上下文节点的**CustomerID**属性。  
  
 在此示例中`attribute` ，是轴， `CustomerID`是节点测试。 **特性**轴的主要节点类型为** \<attribute>**。 因此，如果**CustomerID**是>节点的** \<属性**，则节点测试为 TRUE。 如果上下文节点没有**CustomerID**，则返回一组空节点。  
  
> [!NOTE]  
>  在此 XPath 实现中，如果定位步骤引用** \<元素>** 或未在架构中声明的** \<特性>** 类型，则会生成错误。 这与 MSXML 中的 XPath 实现不同，在 MSXML 中返回空节点集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>轴的缩写语法  
 支持以下位置路径的缩写语法：  
  
-   
  `attribute::` 可缩写为 `@`。  
  
     位置路径 `Customer[@CustomerID="ALFKI"]` 与 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   可以从位置步骤中省略 `child::`。  
  
     因此，**子级**为默认轴。 位置路径 `Customer/Order` 与 `child::Customer/child::Order` 相同。  
  
-   
  `self::node()` 可缩写为一个句点 (.)，`parent::node()` 可缩写为两个句点 (..)。  
  
  
