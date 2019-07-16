---
title: 最短路径 （SQL 图形） |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b4e07c8aa0c7911b02f7df5386c03b1860df38c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035878"
---
# <a name="shortestpath-transact-sql"></a>SHORTEST_PATH (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  指定的图形，这是一个搜索条件搜索以递归方式或重复损坏。 SHORTEST_PATH 可用于在匹配图形节点和边缘表，在 SELECT 语句中。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>最短路径
SHORTEST_PATH 函数允许您查找：    
* 两个给定节点/实体之间最短路径
* 单一源最短路径。
* 从多个源节点到多个目标节点的最短路径。

它采用一种任意长度的字符串模式作为输入并返回两个节点之间存在的最短路径。 此函数仅可在匹配项。 该函数返回任何两个给定节点之间只有一个最短路径。 如果存在，任何对源和目标节点，遍历期间找到第一个函数返回只有一条路径之间的长度相同的两个或多个最短路径。 请注意任意长度的字符串模式，只能在 SHORTEST_PATH 函数内指定。 

请参阅[匹配项 （SQL 图形）](../../t-sql/queries/match-sql-graph.md)语法。 

## <a name="for-path"></a>为路径
路径必须使用与将参与任意长度的字符串模式的 FROM 子句中的任何节点或边界表名称。 路径可以使引擎节点或边界表将返回表示列表的节点或边缘遍历的路径中找到的有序的集合。 不能直接在 SELECT 子句中计划这些表中的属性。 若要将项目从这些表的属性中，图形路径聚合函数必须使用。  

## <a name="arbitrary-length-pattern"></a>任意长度的字符串模式
此模式包含节点和边缘，直到达到所需的节点，或者直到模式中指定的迭代的最大数目必须重复遍历满足。 每次执行查询时，执行这种模式的结果将是节点和边缘从起始节点到结束节点遍历的路径的有序的集合。 这是一个正则表达式样式语法模式并支持以下两个模式限定符：

* **'+'** :重复模式 1 次或多次。 找到最短路径后立即终止。
* **{1,n}** ：重复模式 1到“n”次。 找到最短时，就立即终止。

## <a name="lastnode"></a>LAST_NODE
LAST_NODE() 函数允许链接的两个任意长度的遍历模式。 它可以在方案中使用其中：    
* 在查询中使用多个最短路径模式，并在前面的模式的最后一个节点开始的一种模式。
* 在同一个 LAST_NODE() 合并两个最短路径模式。

## <a name="graph-path-order"></a>图形路径顺序
图形路径顺序引用输出路径中的数据的顺序。 输出路径顺序始终开始跟节点/边缘中的递归部分显示的模式的非递归部分。 在查询优化/执行期间遍历图的顺序与输出中打印的顺序无关。 同样，在递归模式下的箭头方向也不会影响图形路径顺序。 

## <a name="graph-path-aggregate-functions"></a>图形路径聚合函数
由于节点和边缘中涉及到返回的任意长度的字符串模式 （节点和边缘遍历该路径中） 的集合，用户不能项目直接使用传统 tablename.attributename 语法的属性。 对于查询，它在需要时对项目属性值从中间节点或边界表，请在路径遍历，使用下面的图形路径聚合函数：STRING_AGG、 LAST_VALUE、 SUM、 AVG、 MIN、 最大值和计数。 若要在 SELECT 子句中使用这些聚合函数的常规语法是：

```
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="stringagg"></a>STRING_AGG
STRING_AGG 函数采用一个表达式和分隔符作为输入，并返回一个字符串。 用户可以使用此函数在 SELECT 子句中对项目属性从中间节点或边缘中遍历的路径。 

### <a name="lastvalue"></a>LAST_VALUE
可以使用路径遍历，LAST_VALUE 聚合函数的最后一个节点中的属性的项目。 它是错误边缘表别名作为输入提供给此函数中，只有节点表名称或可以使用别名。

**最后一个节点**:最后一个节点是指将出现在遍历，而不考虑匹配谓词中的箭头方向的路径中最后一个节点。 例如： `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`。 下面的路径中的最后一个节点将已访问的最后一个 P 节点。 

而最后一个节点是在此模式的输出关系图路径中的最后一个第 n 个节点： `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
此函数返回遍历的路径中提供的节点/边缘属性值或出现的表达式之和。

### <a name="count"></a>COUNT
此函数返回路径中的所需的节点/边缘属性的非 null 值的数量。 COUNT 函数支持\*节点或边界表的别名使用的运算符。 节点或边界表别名的使用情况\*不明确，将导致错误。

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
返回遍历的路径中提供的节点/边缘属性值或出现的表达式的平均值。

### <a name="min"></a>MIN
从提供的节点/边缘属性值或在遍历路径中出现的表达式返回的最小值。

### <a name="max"></a>MAX
从提供的节点/边缘属性值或在遍历路径中出现的表达式返回的最大值。

## <a name="remarks"></a>备注  
shortest_path 函数只能在匹配项。     
LAST_NODE 仅支持在 shortest_path 内。     
不支持查找加权的最短路径，所有路径或所有最短路径。         
在某些情况下，具有较大的数字的跃点，这会导致更高版本的查询执行时间的查询可能会产生坏的计划。 使用哈希联接提示可能会有帮助。    


## <a name="examples"></a>示例 
我们将 ot 如下所示的示例查询使用节点和边缘表中创建[SQL 图形示例](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>A.  查找 2 的人物之间的最短路径
 在以下示例中，我们发现 Jacob 和 Alice 之间最短路径。 我们将需要 /people/person 节点和从关系图的示例脚本创建 FriendOf 边缘。 

 ```
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  在图中查找从给定的节点到所有其他节点的最短路径。 
 下面的示例中的图形以及 Jacob 从开始到所有人的最短路径查找 Jacob 连接到的所有人员。 

 ```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
 ```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  跃点/遍历从一个人转到另一个关系图中的级别数目进行计数。
 下面的示例查找 Jacob 和 Alice 之间的最短路径，并输出的所需从 Jacob 转到 Alice 的跃点数。 

 ```
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. 查找给定的人员离开 1-3 跃点的用户
下面的示例中图 1-3 跃点离开他查找 Jacob 和他已连接到的所有人之间的最短路径。 

```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. 查找从给定的人员的 2 个跃点的用户
下面的示例查找 Jacob 和关系图中从他的 2 个跃点的人之间的最短路径。 

```
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>请参阅  
 [匹配项 （SQL 图形）](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT（SQL 图形）](../../t-sql/statements/insert-sql-graph.md)]  
 [使用 SQL Server 2017 进行图形处理](../../relational-databases/graphs/sql-graph-overview.md)     
 
