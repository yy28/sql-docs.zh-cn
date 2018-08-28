---
title: CREATE TABLE（SQL 图形）| Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76ad793e7076a5c206f5e26859331746540a7104
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43086050"
---
# <a name="create-table-sql-graph"></a>CREATE TABLE（SQL 图形）
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

以 `NODE` 或 `EDGE` 表的形式创建新 SQL 图形表。 
  
> [!NOTE]   
>  有关标准 Transact-SQL 语句，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。
  
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
本文档仅列出与 SQL 图形相关的参数。 有关受支持参数的完整列表和说明，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)

 database_name    
 要在其中创建表的数据库的名称。 database_name 须指定现有数据库的名称。 如果未指定，则 database_name 默认为当前数据库。 当前连接的登录名必须与 database_name 所指定数据库中的一个现有用户 ID 关联，并且该用户 ID 必须具有 CREATE TABLE 权限。  
  
 schema_name    
 新表所属架构的名称。  
  
 *table_name*    
 是节点或边界表的名称。 表名必须遵循有关[标识符](../../relational-databases/databases/database-identifiers.md)的规则。 除了本地临时表名（以单个数字符号 (#) 为前缀的名称）不能超过 116 个字符外，table_name 最多可包含 128 个字符。  
  
 NODE   
 创建节点表。

 EDGE  
 创建边界表。  
  
## <a name="remarks"></a>Remarks  
不支持以节点或边界表的形式创建临时表。  

不支持以临时表的形式创建节点或边界表。

节点或边界表不支持延伸数据库。

节点或边界表不能是外部表（对于图形表没有 polybase 支持）。 
  
 
## <a name="examples"></a>示例  
  
### <a name="a-create-a-node-table"></a>A. 创建 `NODE` 表
 下面的示例演示如何创建 `NODE` 表

```
 CREATE TABLE Person (
        ID INTEGER PRIMARY KEY, 
        name VARCHAR(100), 
        email VARCHAR(100)
 ) AS NODE;
```

### <a name="b-create-an-edge-table"></a>B. 创建 `EDGE` 表
下面的示例演示如何创建 `EDGE` 表

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
 [INSERT（SQL 图形）](../../t-sql/statements/insert-sql-graph.md)]  
 [使用 SQL Server 2017 进行图形处理](../../relational-databases/graphs/sql-graph-overview.md)

