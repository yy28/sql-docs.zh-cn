---
title: 图形处理与 SQL Server 和 Azure SQL 数据库 |Microsoft 文档
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: cc6951aa90bf71cb415770f30352120a529bcde1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>图形处理与 SQL Server 和 Azure SQL 数据库
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供对多对多关系建模图数据库功能。 关系图关系都已集成到[!INCLUDE[tsql-md](../../includes/tsql-md.md)]和接收的使用好处[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为基础数据库管理系统。


## <a name="what-is-a-graph-database"></a>什么是图形数据库  
图形数据库是一个集合节点 （或顶点） 和边缘 （或关系）。 节点表示实体 （例如，一个人或组织），边缘表示连接 （如组件或好友） 的两个节点之间的关系。 节点和边缘可能具有与之关联的属性。 此处提供一些功能，使关系图数据库唯一：  
-   边缘或关系是 Graph 数据库中的第一类实体，可以具有属性与其关联。 
-   单个的边缘可以灵活地连接 Graph 数据库中的多个节点。
-   可以轻松地展现模式匹配和多跃点导航查询。
-   可以轻松地展现传递闭包和多态查询。

## <a name="when-to-use-a-graph-database"></a>何时使用图形数据库

没有任何关系图的数据库可以实现，这不能使用关系数据库来实现。 但是，关系图数据库可以更加轻松地 express 将某些类型的查询。 此外，使用特定的优化，某些查询可能更好地执行。 选择一种您决定可以基于以下因素：  
-   你的应用程序具有层次结构数据。 HierarchyID 数据类型可以用于实现层次结构，但它具有一些限制。 例如，它不允许你可以存储多个父节点。
-   你的应用程序具有复杂的多对多关系;当应用程序升级后，将添加新关系。
-   你需要分析互连的数据和关系。

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>关系图中引入的功能 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
我们正在启动将关系图扩展添加到 SQL Server，以简化存储和查询关系图数据。 以下功能已在第一个版本中引入。 


### <a name="create-graph-objects"></a>创建图形对象
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] 扩展将允许用户创建节点或边缘表。 节点和边缘可以具有与它们关联的属性。 作为表存储节点和边缘，支持对节点或边缘表关系的表支持的所有操作。 以下是示例：  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![人员好友表](../../relational-databases/graphs/media/person-friends-tables.png "人员节点和朋友边缘表")  
节点和边缘作为表存储  

### <a name="query-language-extensions"></a>查询语言扩展  
新`MATCH`子句引入以支持模式匹配和多跃点通过 graph 的导航。 `MATCH`函数使用 ASCII 图文样式语法中的模式匹配。 例如：  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>在完全集成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]引擎 
Graph 扩展完全集成在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]引擎。 我们使用相同的存储引擎、 元数据，查询处理器等来存储和查询关系图数据。 这使用户能够跨其关系图和单个查询中的关系数据进行查询。 用户也可以从与其他组合图功能受益[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]技术与列存储中，实现高可用性，R 服务，相似等。SQL graph 数据库还支持所有的安全和合规性功能适用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
 
### <a name="tooling-and-ecosystem"></a>工具和生态系统  
用户从现有工具和生态系统中受益，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供。 备份和还原，之类的工具导入和导出，现成的 BCP 只需工作。 其他工具或如 SSIS、 SSRS 或 PowerBI 服务将使用 graph 表，它们使用关系表的方式。
 
 ## <a name="next-steps"></a>后续步骤  
读取[SQL Graph 数据库-体系结构](./sql-graph-architecture.md)
   

