---
title: SQL 图形体系结构 |Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 49a0d942fd4d738b31d71d44fc74392469d047c2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39546397"
---
# <a name="sql-graph-architecture"></a>SQL 图形体系结构  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

了解如何构建 SQL 图形。 了解基础知识将使其更易理解 SQL 图形的其他文章。
 
## <a name="sql-graph-database"></a>SQL 图形数据库
用户可以创建每个数据库的一个关系图。 关系图是节点和边界表的集合。 可以在数据库中的任何架构下创建节点或边界表，但它们都属于一个逻辑关系图。 节点表是节点的相似类型的集合。 例如，Person 节点表包含属于关系图的所有人员节点。 同样，边缘表是边缘的相似类型的集合。 例如，好友边缘表具有将一个 Person 连接到另一个人的所有边缘。 由于节点和边缘表中存储，在节点或边界表上支持大多数常规表上支持的操作。 
 
 
![sql 图形体系结构](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql 图形数据库体系结构")   

图 1: SQL 图形数据库体系结构
 
## <a name="node-table"></a>节点表
节点表表示关系图架构中的实体。 每次节点将创建一个表，以及用户定义列中，隐式`$node_id`创建列后，可唯一标识数据库中给定的节点。 中的值`$node_id`自动生成的是的组合`object_id`的该节点表和内部生成的 bigint 值。 但是，当`$node_id`选择列，显示中的 JSON 字符串形式的计算的值。 此外，`$node_id`是伪列，映射到在其中的十六进制字符串与内部名称。 当选择`$node_id`从表中，列名称将显示为`$node_id_<hex_string>`。 在查询中使用伪列名称是推荐的方法来查询内部`$node_id`应避免列和十六进制字符串，使用内部名称。

建议用户创建唯一约束或索引上`$node_id`处的节点表，但如果其中一个不创建时间的列创建，默认值自动创建唯一的非聚集索引。 但是，在基础内部列上创建图表伪列上的任何索引。 也就是说，在创建的索引`$node_id`列中，会出现在内部`graph_id_<hex_string>`列。   


## <a name="edge-table"></a>边缘表
边缘表表示关系图中的关系。 边缘始终定向，并连接两个节点。 边缘表，对多对多关系建模关系图中的用户。 边缘表可能会或可能没有任何用户定义的属性中。 每次创建边缘表时，以及用户定义属性中，边缘表中创建三个隐式列：

|列名    |Description  |
|---   |---  |
|`$edge_id`   |唯一标识数据库中的一个给定的边缘。 它是生成的列和值是边缘表和内部生成的 bigint 值的 object_id 的组合。 但是，当`$edge_id`选择列，显示中的 JSON 字符串形式的计算的值。 `$edge_id` 是一个伪列，映射到在其中的十六进制字符串与内部名称。 当选择`$edge_id`从表中，列名称将显示为`$edge_id_\<hex_string>`。 在查询中使用伪列名称是推荐的方法来查询内部`$edge_id`应避免列和十六进制字符串，使用内部名称。 |
|`$from_id`   |存储`$node_id`节点从边缘在哪里产生。  |
|`$to_id`   |存储`$node_id`的节点，边缘会终止。 |

给定的边缘可以连接的节点中插入的数据受到`$from_id`和`$to_id`列。 在第一个版本中，不能在边缘表，以将其限制为从连接的节点的任何两个类型上定义约束。 也就是说，边缘可以连接的图形，而不考虑其类型中任何两个节点。

类似于`$node_id`列中，建议用户创建唯一索引或约束上`$edge_id`创建了边缘表，但如果其中一个不是创建时的列，默认值自动创建唯一，非聚集索引此列。 但是，在基础内部列上创建图表伪列上的任何索引。 也就是说，在创建的索引`$edge_id`列中，会出现在内部`graph_id_<hex_string>`列。 此外建议，对于 OLTP 方案，用户在创建索引 (`$from_id`， `$to_id`) 列，用于查找中的边缘方向的速度更快。  

图 2 显示了如何在数据库中存储节点和边界表。 

![朋友的 person 表](../../relational-databases/graphs/media/person-friends-tables.png "/people/person 节点和好友边缘表")   

图 2： 节点和边界表的表示形式



## <a name="metadata"></a>元数据
使用这些元数据视图可以查看的节点或边界表的属性。
 
### <a name="systables"></a>sys.tables
以下新，bit 类型，会将列添加到 SYS。表。 如果`is_node`设置为 1，指示表是节点表并且如果`is_edge`设置为 1，指示表是边界表。
 
|列名 |数据类型 |Description |
|--- |---|--- |
|is_node |bit |1 = 这是节点表 |
|is_edge |bit |1 = 这是一个边缘表 |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns`视图中的其他列`graph_type`和`graph_type_desc`，指示节点和边缘表中列的类型。
 
|列名 |数据类型 |Description |
|--- |---|--- |
|graph_type |ssNoversion |使用一组值的内部列。 值是之间的关系图列 1-8 和其他人的 NULL。  |
|graph_type_desc |nvarchar(60)  |内部使用的一组值的列 |
 
下表列出了有效的值为`graph_type`列

|列的值  |Description  |
|---   |---   |
|@shouldalert  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` 此外将存储在节点或边界表中创建的隐式列的信息。 以下信息可以检索从 sys.columns，但是，用户不能选择这些列从一个节点或边界表。 

节点表中的隐式列  
|列名    |数据类型  |is_hidden  |注释  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |@shouldalert  |内部 graph_id 列  |
|$node_id_\<hex_string> |NVARCHAR   |0  |外部节点 id 列  |

边缘表中的隐式列  
|列名    |数据类型  |is_hidden  |注释  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |@shouldalert  |内部 graph_id 列  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |外部边缘 id 列  |
|from_obj_id_\<hex_string>  |INT    |@shouldalert  |内部从节点对象 id  |
|from_id_\<hex_string>  |bigint |@shouldalert  |从节点 graph_id 内部  |
|$from_id_\<hex_string> |NVARCHAR   |0  |节点 id 从外部  |
|to_obj_id_\<hex_string>    |INT    |@shouldalert  |内部节点对象 id  |
|to_id_\<hex_string>    |bigint |@shouldalert  |内部节点 graph_id  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |外部的节点 id  |
 
### <a name="system-functions"></a>系统函数
添加下列内置函数。 这些功能帮助用户从生成的列中提取信息。 请注意，这些方法将不会验证用户输入。 如果用户指定了无效`sys.node_id`方法将提取的相应部分，并将其返回。 例如，将采用 OBJECT_ID_FROM_NODE_ID`$node_id`作为输入，并将返回 object_id 的表，此节点所属。 
 
|内置   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |从 node_id 提取 object_id  |
|GRAPH_ID_FROM_NODE_ID  |从 node_id 提取 graph_id  |
|NODE_ID_FROM_PARTS |构造从 object_id 和 graph_id node_id  |
|OBJECT_ID_FROM_EDGE_ID |从 edge_id 提取 object_id  |
|GRAPH_ID_FROM_EDGE_ID  |从 edge_id 提取标识  |
|EDGE_ID_FROM_PARTS |构造 edge_id 从 object_id 和标识  |



## <a name="transact-sql-reference"></a>TRANSACT-SQL 参考 
了解[!INCLUDE[tsql-md](../../includes/tsql-md.md)]引入 SQL Server 和 Azure SQL 数据库中的扩展，以便创建和查询图形对象。 查询语言扩展帮助查询和遍历图形使用 ASCII 图表语法。
 
### <a name="data-definition-language-ddl-statements"></a>数据定义语言 (DDL) 语句
|任务   |相关的主题  |说明
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` 现已扩展为支持创建表 AS 节点或 AS 边界。 请注意，边缘表可能会或可能没有任何用户定义的属性。  |
|ALTER TABLE    |[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)|可以更改节点和边缘表的关系表，使用的相同方式`ALTER TABLE`。 用户可以添加或修改用户定义的列、 索引或约束。 但是，更改内部图表列，喜欢`$node_id`或`$edge_id`，将导致错误。  |
|CREATE INDEX   |[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)  |用户可以对伪列和节点和边缘表中的用户定义列创建索引。 支持所有索引类型，包括聚集和非聚集列存储索引。  |
|DROP TABLE |[删除表&#40;Transact SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |在关系表，使用的相同方式删除节点和边界表`DROP TABLE`。 但是，在此版本中，任何约束，以确保没有边缘指向已删除的节点和支持级联的删除边缘节点或节点表在删除时。 建议删除节点表后，如果用户删除该节点表手动维护完整性的关系图中的节点连接到任何边缘。  |


### <a name="data-manipulation-language-dml-statements"></a>数据操作语言 (DML) 语句
|任务   |相关的主题  |说明
|---  |---  |---  |
|Insert |[INSERT (Transact-SQL)](../../t-sql/statements/insert-sql-graph.md)|插入节点表与关系表中插入无异。 值`$node_id`自动生成列。 尝试插入中的值`$node_id`或`$edge_id`列将导致错误。 用户必须提供相应的值`$from_id`和`$to_id`插入边缘表时的列。 `$from_id` 并`$to_id`是`$node_id`给定的边连接节点的值。  |
|删除 | [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)|可以在相同的方式删除节点或边界表中的数据，因为从关系表中删除它。 但是，在此版本中，任何约束，以确保没有边缘指向已删除的节点和支持级联的删除边缘节点在删除时。 建议，无论何时删除节点，到该节点的所有连接边，也将删除维护的关系图的完整性。  |
|UPDATE |[UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)  |可以使用 UPDATE 语句更新用户定义列中的值。 更新内部图表列中， `$node_id`， `$edge_id`，`$from_id`和`$to_id`不允许。  |
|MERGE |[MERGE (Transact-SQL)](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 将节点或边界表不支持语句。  |


### <a name="query-statements"></a>查询语句
|任务   |相关的主题  |说明
|---  |---  |---  |
|SELECT |[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)|节点和边缘表作为内部存储，因此在节点和边界表上支持大多数 SQL Server 或 Azure SQL 数据库中的表支持的操作  |
|MATCH  | [匹配&#40;Transact SQL&#41;](../../t-sql/queries/match-sql-graph.md)|引入了匹配项的内置支持模式匹配和遍历关系图。  |



## <a name="limitations-and-known-issues"></a>限制和已知问题  
有在此版本中的节点和边界表的某些限制：
* 本地或全局临时表不能为节点或边界表。
* 表类型和表变量不能声明为节点或边界表。 
* 不能为系统版本控制临时表创建节点和边界表。   
* 节点和边界表不能为内存优化表。  
* 用户不能更新的 $from_id 和 $to_id 列使用 UPDATE 语句的边缘。 若要更新的节点的边连接，用户将必须插入指向新节点的新边缘和删除前一个。
* 跨数据库不支持图形对象上的查询。 


## <a name="next-steps"></a>后续步骤
若要开始使用新语法，请参阅[SQL 关系图数据库的示例](./sql-graph-sample.md)
 

