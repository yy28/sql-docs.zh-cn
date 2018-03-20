---
title: "SQL Graph 体系结构 |Microsoft 文档"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: graphs
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: 
caps.latest.revision: 
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 887ac78e70d529c404ee2ed3088f088ed53e4a54
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="sql-graph-architecture"></a>SQL Graph 体系结构  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

了解如何构建 SQL 关系图。 了解基础知识将更加轻松地了解其他 SQL Graph 文章。
 
## <a name="sql-graph-database"></a>SQL 图形数据库
用户可以创建每个数据库的一个关系图。 关系图是一系列节点和边缘表。 可在数据库中，任何架构下创建节点或边缘表，但它们都属于一个逻辑图形。 节点表是相似类型的节点的集合。 例如，Person 节点表包含属于关系图的所有人员节点。 同样，边缘表是边缘的相似类型的集合。 例如，好友边缘表包含连接到其他人的人员的所有边缘。 由于节点和边缘存储在表中，在节点或边缘表上支持大多数普通表上支持的操作。 
 
 
![sql graph 体系结构](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql graph 数据库体系结构")   

图 1: SQL Graph 数据库体系结构
 
## <a name="node-table"></a>节点表
节点表都表示图架构中的实体。 每次节点创建了一个表，以及用户定义的列，一种隐式`$node_id`创建列后，它唯一地标识在数据库中给定的节点。 中的值`$node_id`自动生成，组合`object_id`节点该表和内部生成的 bigint 值。 但是，当`$node_id`选择列，显示的 JSON 字符串形式的计算的值。 此外，`$node_id`是伪列，映射到在其中的十六进制字符串与内部名称。 当选择`$node_id`表中的列名称将显示为`$node_id_<hex_string>`。 在查询中使用伪列名称是推荐的方法来查询内部`$node_id`应避免列和十六进制字符串，使用内部名称。

建议用户创建唯一约束或索引上`$node_id`创建的节点表中，但如果其中一个不是创建时的列，的默认自动创建唯一，非聚集索引。 但是，在基础内部列上创建上图伪列任何索引。 也就是说，在创建索引`$node_id`列中，将出现在内部`graph_id_<hex_string>`列。   


## <a name="edge-table"></a>边缘表
边缘表表示关系图中的关系。 边缘始终将定向和连接两个节点。 边缘表允许对多对多关系建模关系图中的用户。 边缘表可能或可能没有任何用户定义的属性中。 每次创建边缘表时，以及用户定义属性中，边缘表中创建三个隐式列：

|列名    |Description  |
|---   |---  |
|`$edge_id`   |唯一标识数据库中的一个给定的边缘。 它是生成的列和值是 object_id 边缘表和内部生成的 bigint 值的组合。 但是，当`$edge_id`选择列，显示的 JSON 字符串形式的计算的值。 `$edge_id` 是伪列，映射到在其中的十六进制字符串与内部名称。 当选择`$edge_id`表中的列名称将显示为`$edge_id_\<hex_string>`。 在查询中使用伪列名称是推荐的方法来查询内部`$edge_id`应避免列和十六进制字符串，使用内部名称。 |
|`$from_id`   |存储`$node_id`的节点，边缘的来源位置。  |
|`$to_id`   |存储`$node_id`节点，并从该处边缘终止。 |

给定的边缘可以连接的节点由在中插入数据控制`$from_id`和`$to_id`列。 在第一个版本中，则不可以定义在边缘表，以将其限制连接任何两个类型的节点上的约束。 也就是说，一条边可以连接在图中，而不管其类型的任何两个节点。

类似于`$node_id`列中，建议用户创建唯一索引或约束上`$edge_id`创建了边缘表，但如果其中一个不是创建时的列，的默认对自动创建唯一，非聚集索引此列。 但是，在基础内部列上创建上图伪列任何索引。 也就是说，在创建索引`$edge_id`列中，将出现在内部`graph_id_<hex_string>`列。 此外建议，对于 OLTP 方案，用户上创建索引 (`$from_id`， `$to_id`) 列，更快查找边缘方向。  

图 2 显示节点和边缘表在数据库中的存储方式。 

![人员好友表](../../relational-databases/graphs/media/person-friends-tables.png "人员节点和朋友边缘表")   

图 2： 节点和边缘表表示形式



## <a name="metadata"></a>元数据
使用这些元数据视图可查看的节点或边缘表的属性。
 
### <a name="systables"></a>sys.tables
以下新，位类型，会将列添加到 SYS。表。 如果`is_node`设置为 1，指示表为节点表并且如果`is_edge`设置为 1，指示表为边缘表。
 
|列名 |数据类型 |Description |
|--- |---|--- |
|is_node |bit |1 = 这是一个节点表 |
|is_edge |bit |1 = 这是一个边缘表 |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns`视图中的其他列`graph_type`和`graph_type_desc`，指示节点和边缘表中的列的类型。
 
|列名 |数据类型 |Description |
|--- |---|--- |
|graph_type |int |具有一组值的内部列。 值可以介于 1-8 graph 列和其他人的 NULL。  |
|graph_type_desc |nvarchar(60)  |内部列组的值 |
 
下表列出的有效值`graph_type`列

|列的值  |Description  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` 此外将存储在节点或边缘表中创建的隐式列的信息。 下列信息可以检索从 sys.columns，但是，用户无法选择这些列从节点或边缘表。 

节点表中的隐式列  
|列名    |数据类型  |is_hidden  |注释  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |内部 graph_id 列  |
|$node_id_\<hex_string> |NVARCHAR   |0  |外部节点 id 列  |

边缘表中的隐式列  
|列名    |数据类型  |is_hidden  |注释  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |内部 graph_id 列  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |外部边缘 id 列  |
|from_obj_id_\<hex_string>  |INT    |1  |内部从节点对象 id  |
|from_id_\<hex_string>  |bigint |1  |从节点 graph_id 内部  |
|$from_id_\<hex_string> |NVARCHAR   |0  |外部从节点 id  |
|to_obj_id_\<hex_string>    |INT    |1  |内部节点对象 id  |
|to_id_\<hex_string>    |bigint |1  |内部节点 graph_id  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |外部的节点 id  |
 
### <a name="system-functions"></a>系统函数
添加的下列内置函数。 这些将帮助从生成的列中提取信息的用户。 请注意，这些方法将不会验证用户输入。 如果用户指定了无效`sys.node_id`方法将提取的相应部分，并将其返回。 例如，将占用 OBJECT_ID_FROM_NODE_ID`$node_id`作为输入，并将返回 object_id 此节点所属的表。 
 
|内置   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |从通过 node_id 提取 object_id  |
|GRAPH_ID_FROM_NODE_ID  |从通过 node_id 提取 graph_id  |
|NODE_ID_FROM_PARTS |构造从 object_id 和 graph_id node_id  |
|OBJECT_ID_FROM_EDGE_ID |从 edge_id 提取 object_id  |
|GRAPH_ID_FROM_EDGE_ID  |从 edge_id 提取标识  |
|EDGE_ID_FROM_PARTS |构造 edge_id 从 object_id 和标识  |



## <a name="transact-sql-reference"></a>TRANSACT-SQL 参考 
了解[!INCLUDE[tsql-md](../../includes/tsql-md.md)]扩展 SQL Server 和 Azure SQL 数据库中引入，允许创建和查询关系图的对象。 查询语言扩展帮助查询和遍历该图使用 ASCII 艺术作品语法。
 
### <a name="data-definition-language-ddl-statements"></a>数据定义语言 (DDL) 语句
|任务   |相关的主题  |说明
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` 现已扩展来支持创建 AS 节点或 AS 边缘表。 请注意边缘表可能或可能没有任何用户定义属性。  |
|ALTER TABLE    |[ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)|节点和边缘表可以更改关系表，使用的相同方式`ALTER TABLE`。 用户可以添加或修改用户定义的列、 索引或约束。 但是，更改内部 graph 列，就像`$node_id`或`$edge_id`，将导致错误。  |
|CREATE INDEX   |[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)  |用户可以对伪列和用户定义的节点和边缘表的列创建索引。 支持所有索引类型，包括聚集和非聚集列存储索引。  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |可以删除节点和边缘表的关系表，使用的相同方式`DROP TABLE`。 但是，在此版本中，任何约束，以确保没有边缘指向已删除的节点，并支持的边缘，在删除节点或节点表时的级联的删除。 建议，如果删除节点表后，则用户将断开任何连接到该节点表手动维护的关系图的完整性中节点的边缘。  |


### <a name="data-manipulation-language-dml-statements"></a>数据操作语言 (DML) 语句
|任务   |相关的主题  |说明
|---  |---  |---  |
|Insert |[INSERT (Transact-SQL)](../../t-sql/statements/insert-sql-graph.md)|将插入到节点表是将插入到关系表没有什么不同。 值`$node_id`自动生成列。 尝试插入中的值`$node_id`或`$edge_id`列将导致错误。 用户必须提供值`$from_id`和`$to_id`时将插入到边缘表的列。 `$from_id` 和`$to_id`是`$node_id`给定的边连接节点的值。  |
|DELETE | [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)|可以在相同的方式中删除节点或边缘表中的数据，因为它从关系表中删除。 但是，在此版本中，任何约束，以确保没有边缘指向已删除的节点，并支持的边缘，在删除节点时的级联的删除。 建议，每当删除节点时，与该节点的所有连接边缘也将被删除，若要维护的关系图的完整性。  |
|UPDATE |[UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)  |可以使用 UPDATE 语句更新中用户定义的列的值。 更新的内部关系图列中， `$node_id`， `$edge_id`，`$from_id`和`$to_id`不允许。  |
|MERGE |[MERGE (Transact-SQL)](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 在节点或边缘表上不支持语句。  |


### <a name="query-statements"></a>查询语句
|任务   |相关的主题  |说明
|---  |---  |---  |
|SELECT |[SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)|节点和边缘表作为内部存储，因此在的节点和边缘表上支持大多数 SQL Server 或 Azure SQL 数据库中的表上支持的操作  |
|MATCH  | [匹配&#40;Transact SQL&#41;](../../t-sql/queries/match-sql-graph.md)|引入了匹配内置来支持模式匹配和遍历关系图。  |



## <a name="limitations-and-known-issues"></a>限制和已知的问题  
有一定的限制对此版本中的节点和边缘表：
* 本地或全局临时表不能为节点或边缘表。
* 表类型和表变量不能声明为节点或边缘表。 
* 不能为系统版本控制临时表创建节点和边缘表。   
* 节点和边缘表不能为内存优化表。  
* 用户不能更新的 $from_id 和 $to_id 列使用 UPDATE 语句的边缘。 若要更新边连接的节点，用户将必须插入指向新节点的新边缘，则删除前一个。
* 跨数据库不支持图形对象上的查询。 


## <a name="next-steps"></a>后续步骤
若要开始使用新的语法，请参阅[SQL Graph 数据库-示例](./sql-graph-sample.md)
 

