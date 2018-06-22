---
title: 指定的位置路径 (SQLXML 4.0) 中的节点测试 |Microsoft 文档
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
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ca3eff7a8d915588d632dc12ff94e42d946d8aad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014741"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路径中指定节点测试 (SQLXML 4.0)
  节点测试指定根据位置步骤选择的节点类型。 每个轴（`child`、`parent`、`attribute` 或 `self`）都具有主要节点类型。 有关`attribute`轴，主体数据库节点类型是**\<属性 >**。 有关`parent`， `child`，和`self`轴，主体数据库节点类型是**\<元素 >**。  
  
> [!NOTE]  
>  不支持通配符节点测试 *（例如 `child::*`）。  
  
## <a name="node-test-example-1"></a>节点测试： 示例 1  
 位置路径`child::Customer`选择**\<客户 >** 元素的上下文节点的子级。  
  
 在本示例中，`child` 是轴，`Customer` 是节点测试。 主体数据库节点类型`child`轴**\<元素 >**。 因此，节点测试为 TRUE，如果**\<客户 >** 节点是**\<元素 >** 节点。 如果上下文节点没有**\<客户 >** 子级，则返回节点的空集。  
  
## <a name="node-test-example-2"></a>节点测试：示例 2  
 位置路径`attribute::CustomerID`选择**CustomerID**上下文节点属性。  
  
 在示例中，`attribute`是轴和`CustomerID`是节点的测试。 主体的节点类型`attribute`轴**\<属性 >**。 因此，节点测试为 TRUE，如果**CustomerID**是**\<属性 >** 节点。 如果上下文节点没有**CustomerID**，返回节点的空集。  
  
> [!NOTE]  
>  在此实现中的 XPath，如果定位步骤引用**\<元素 >** 或**\<属性 >** 不在生成错误的架构中声明的类型。 这与 MSXML 中的 XPath 实现不同，在 MSXML 中返回空节点集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>轴的缩写语法  
 支持以下位置路径的缩写语法：  
  
-   `attribute::` 可缩写为 `@`。  
  
     位置路径 `Customer[@CustomerID="ALFKI"]` 与 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   可以从位置步骤中省略 `child::`。  
  
     因此，`child` 为默认轴。 位置路径 `Customer/Order` 与 `child::Customer/child::Order` 相同。  
  
-   `self::node()` 可缩写为一个句点 (.)，`parent::node()` 可缩写为两个句点 (..)。  
  
  