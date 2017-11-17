---
title: "创建表 （SQL 图形） |Microsoft 文档"
ms.custom: 
ms.date: 05/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL_GRAPH_TSQL
- TABLE
- CREATE_TABLE_TSQL
- NODE
- NODE_TSQL
- AS_NODE
- AS_NODE_TSQL
- EDGE
- EDGE_TSQL
- AS_EDGE
- AS_EDGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- graph
- SQL graph
- CREATE TABLE SQL graph
- NODE
- EDGE
- SQL graph, CREATE TABLE statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c32a8c4f683f20c4384089c1d2552614090f9b3d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-table-sql-graph"></a>创建表 （SQL 图形）
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

创建新的 SQL graph 表为`NODE`或`EDGE`表。 
  
> [!NOTE]   
>  有关标准 TRANSACT-SQL 语句，请参阅[CREATE TABLE (TRANSACT-SQL)](../../t-sql/statements/create-table-transact-sql.md)。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE TABLE   
    [ database_name . [ schema_name ] . | schema_name . ] table_name   
    ( { <column_definition> } [ ,...n ] )   
    AS [ NODE | EDGE ]
[ ; ]  
```  
  
  
## <a name="arguments"></a>参数  
本文档列出了仅与 SQL 图形相关的参数。 有关完整列表和支持的参数的说明，请参阅[CREATE TABLE (TRANSACT-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 *database_name*    
 要在其中创建表的数据库的名称。 *database_name*必须指定现有的数据库的名称。 如果未指定， *database_name*默认为当前数据库。 当前连接的登录名必须与指定的数据库中的现有用户 ID 相关联*database_name*，并且该用户 ID 必须具有 CREATE TABLE 权限。  
  
 *schema_name*    
 新表所属架构的名称。  
  
 *table_name*    
 是节点或边缘表的名称。 表名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 *table_name*最多 128 个字符，本地临时表名称除外 (名称前加上以单个数字符号 （#）)，不能超过 116 个字符。  
  
 节点   
 创建节点表。

 边缘  
 创建边缘表。  
  
## <a name="remarks"></a>注释  
不支持创建临时表作为节点或边缘表。  

不支持创建节点或边缘表作为临时表。

节点或边缘表不支持延伸数据库。

节点或边缘表不能为外部表 （关系图表不 polybase 支持）。 
  
 
## <a name="examples"></a>示例  
  
### <a name="a-create-a-node-table"></a>A. 创建`NODE`表
 下面的示例演示如何创建`NODE`表

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. 创建`EDGE`表
下面的示例演示如何创建`EDGE`表

```
 CREATE TABLE friends (
    id integer PRIMARY KEY,
    start_date date
 ) AS EDGE;

```

```
 -- Create a likes edge table, this table does not have any user defined attributes   
 CREATE TABLE likes AS EDGE;

```


## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [INSERT （SQL 图形）](../../t-sql/statements/insert-sql-graph.md)]  
 [使用 SQL Server 2017 处理的关系图](../../relational-databases/graphs/sql-graph-overview.md)


