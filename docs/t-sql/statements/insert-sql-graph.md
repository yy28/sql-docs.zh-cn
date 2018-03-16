---
title: "INSERT（SQL 图形）| Microsoft Docs"
description: "SQL 图形节点或边缘表的 INSERT 语法。"
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
caps.latest.revision: 
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6bac7f1d7da67f319a9c84425b370bb61a35ca19
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="insert-sql-graph"></a>INSERT（SQL 图形）
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 `node` 或 `edge` 表格添加一行或多行。 

> [!NOTE]   
>  有关标准 TRANSACT-SQL 语句，请参阅 [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>插入节点表语法 
插入节点表的语法与常规表的相同。 

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
 本文档介绍与 SQL 图形相关的参数。 有关 INSERT 语句中受支持参数的完整列表和说明，请参阅 [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 一个可选的关键字，可将它用在 `INSERT` 和目标表之间。  
  
 search_condition_with_match   
 插入节点或边缘表时，可在子查询中使用 `MATCH` 子句。 有关 `MATCH` 语句的语法，请参阅 [GRAPH MATCH (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)

 graph_search_pattern   
 提供给 `MATCH` 子句作为图形谓词的一部分的搜索模式。

 edge_table_column_list   
 插入边时，用户必须提供 `$from_id` 和 `$to_id` 的值。 如果未提供值或这些列中插入了 NULL，则将返回一个错误。 
  

## <a name="remarks"></a>Remarks  
插入节点表与插入任何关系表相同。 会自动生成 $node_id 列的值。

插入边缘表时，用户必须提供 `$from_id` 和 `$to_id` 列的值。   

节点表的 BULK 插入与关系表的保持相同。

批量插入边缘表之前，必须导入节点表。 然后才可从节点表的 `$node_id` 列中提取 `$from_id` 和 `$to_id` 的值，并将其作为边插入。 

  
### <a name="permissions"></a>权限  
 需要对目标表具有 INSERT 权限。  
  
 默认情况下，将 INSERT 权限授予 sysadmin 固定服务器角色成员、db_owner 和 db_datawriter 固定数据库角色成员以及表所有者。 sysadmin、db_owner 和 db_securityadmin 角色成员和表所有者可以将权限转让给其他用户。  
  
 若要使用 OPENROWSET 函数 BULK 选项执行 INSERT，必须是 sysadmin 固定服务器角色成员或 bulkadmin 固定服务器角色成员。  
  

## <a name="examples"></a>示例  
  
#### <a name="a--insert-into-node-table"></a>A.  插入节点表  
 以下示例创建 Person 节点表，并向该表插入 2 个行。

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  插入边缘表  
 以下示例创建友元边缘表，并向表中插入一条边。

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>另请参阅  
 [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [使用 SQL Server 2017 进行图形处理](../../relational-databases/graphs/sql-graph-overview.md)  


