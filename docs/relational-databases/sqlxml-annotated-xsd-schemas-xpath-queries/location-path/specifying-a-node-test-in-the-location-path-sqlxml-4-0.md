---
title: 指定节点测试中的位置路径 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 60cd7dcbeed6356165c3bd78ff6516667dac61c7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555877"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>在位置路径中指定节点测试 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  节点测试指定根据位置步骤选择的节点类型。 每个轴 (**子**，**父**，**特性**，或者**自助**) 具有主要节点类型。 有关**特性**轴，主要节点类型是**\<属性 >**。 有关**父**，**子**，并**自助**轴，主要节点类型是**\<元素 >**。  
  
> [!NOTE]  
>  不支持通配符节点测试 *（例如 `child::*`）。  
  
## <a name="node-test-example-1"></a>节点测试： 示例 1  
 位置路径`child::Customer`中选择**\<客户 >** 上下文节点的子元素。  
  
 在本示例中，`child` 是轴，`Customer` 是节点测试。 主要节点类型**子**轴是**\<元素 >**。 因此，如果节点测试为 TRUE **\<客户 >** 节点是**\<元素 >** 节点。 如果上下文节点没有**\<客户 >** 子级，则返回空节点集。  
  
## <a name="node-test-example-2"></a>节点测试：示例 2  
 位置路径`attribute::CustomerID`中选择**CustomerID**上下文节点的属性。  
  
 在示例中，`attribute`是轴和`CustomerID`是节点测试。 主要节点类型**特性**轴是**\<属性 >**。 因此，如果节点测试为 TRUE **CustomerID**是**\<属性 >** 节点。 如果上下文节点没有**CustomerID**，返回空节点集。  
  
> [!NOTE]  
>  在此实现中的 XPath，如果定位步骤所引用的**\<元素 >** 或**\<属性 >** 不在生成错误的架构中声明的类型。 这与 MSXML 中的 XPath 实现不同，在 MSXML 中返回空节点集。  
  
## <a name="abbreviated-syntax-for-the-axes"></a>轴的缩写语法  
 支持以下位置路径的缩写语法：  
  
-   `attribute::` 可缩写为 `@`。  
  
     位置路径 `Customer[@CustomerID="ALFKI"]` 与 `child::Customer[attribute::CustomerID="ALFKI"]` 相同。  
  
-   可以从位置步骤中省略 `child::`。  
  
     因此，**子**是默认轴。 位置路径 `Customer/Order` 与 `child::Customer/child::Order` 相同。  
  
-   `self::node()` 可缩写为一个句点 (.)，`parent::node()` 可缩写为两个句点 (..)。  
  
  
