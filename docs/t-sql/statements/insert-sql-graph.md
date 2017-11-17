---
title: "INSERT （SQL 图形） |Microsoft 文档"
description: "插入 SQL Graph 节点或边缘表的语法。"
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e694d89efef130d2abcd5cd6424e2be576ef09de
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="insert-sql-graph"></a>INSERT （SQL 图形）
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  添加一个或多个行`node`或`edge`表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 

> [!NOTE]   
>  有关标准 TRANSACT-SQL 语句，请参阅[插入表 (Transact SQL)](../../t-sql/statements/insert-transact-sql.md)。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>将插入节点表语法 
将插入到节点表的语法是相同的常规表。 

```  
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>参数  
 本文档介绍与 SQL 图形相关的自变量。 有关完整列表和 INSERT 语句中支持的参数的说明，请参阅[插入表 (TRANSACT-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 是可以之间使用的可选关键字`INSERT`和目标表。  
  
 *search_condition_with_match*   
 `MATCH`在插入节点或边缘表时，可以在子查询使用子句。 有关`MATCH`语句的语法，请参阅[GRAPH 匹配 (TRANSACT-SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 搜索模式提供给`MATCH`graph 谓词的一部分的子句。

 *edge_table_column_list*   
 用户必须提供值`$from_id`和`$to_id`时将插入到一条边。 如果未提供一个值或 null 值插入这些列，将返回错误。 
  

## <a name="remarks"></a>注释  
将插入到一个节点是与将插入到任何关系的表相同。 会自动生成的 $node_id 列的值。

时将插入到边缘表，用户必须提供值`$from_id`和`$to_id`列。   

大容量插入节点表为保持相同的关系表。

在大容量插入边缘表之前, 必须导入节点表。 值为`$from_id`和`$to_id`然后可以从提取`$node_id`节点表的列和作为边缘插入。 

  
### <a name="permissions"></a>Permissions  
 需要对目标表具有 INSERT 权限。  
  
 插入权限仅默认授予的成员**sysadmin**固定服务器角色、 **db_owner**和**db_datawriter**固定数据库角色和表所有者。 成员**sysadmin**， **db_owner**，和**db_securityadmin**角色和表所有者可将权限传输到其他用户。  
  
 若要执行插入使用 OPENROWSET 函数 BULK 选项，你必须**sysadmin**固定的服务器角色或**bulkadmin**固定的服务器角色。  
  

## <a name="examples"></a>示例  
  
#### <a name="a--insert-into-node-table"></a>A.  将插入节点表  
 下面的示例创建 Person 节点表，并将 2 行插入到该表。

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  边缘表中插入  
 下面的示例创建友元边缘表，并向表中插入一条边。

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>另请参阅  
 [插入 TABLE &#40;Transact SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [使用 SQL Server 2017 处理的关系图](../../relational-databases/graphs/sql-graph-overview.md)  



