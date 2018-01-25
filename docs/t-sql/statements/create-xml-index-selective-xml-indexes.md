---
title: "创建 XML 索引 （选择性 XML 索引） |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 1f510151-41d5-45c2-9cd0-b1ca0246fffe
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0cd1c2dd0c77409768e8ea7838724ca4d6b827e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-xml-index-selective-xml-indexes"></a>CREATE XML INDEX（选择性 XML 索引）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  在已通过现有选择性 XML 索引建立索引的单个路径上创建新的辅助选择性 XML 索引。 您还可以创建主要选择性 XML 索引。 有关信息，请参阅[Create、 Alter 和 Drop 选择性 XML 索引](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE XML INDEX index_name  
    ON <table_object> ( xml_column_name )  
    USING XML INDEX sxi_index_name  
    FOR ( <xquery_or_sql_values_path> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
  
<xquery_or_sql_values_path>::=   
<path_name>   
  
<path_name> ::=   
character string literal  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
xmlnamespace_uri AS xmlnamespace_prefix  
  
<index_options> ::=   
(    
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> 参数  
 *index_name*  
 要创建的新索引的名称。 索引名称在一个表，必须是唯一的但不是需要在数据库中是唯一。 索引名称必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 ON  *\<table_object >*是包含索引的 XML 列的表。 您可以使用下列格式：  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
 *xml_column_name*  
 包含要建立索引的路径的 XML 列的名称。  
  
 USING XML INDEX *sxi_index_name*  
 现有选择性 XML 索引的名称。  
  
 有关**(** \<xquery_or_sql_values_path > **)**是要在其中创建辅助选择性 XML 索引建立索引的路径的名称。 要建立索引的路径是从 CREATE SELECTIVE XML INDEX 语句分配的名称。 有关详细信息，请参阅 [CREATE SELECTIVE XML INDEX (Transact-SQL)](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。  
  
 与\<index_options > 有关索引选项的信息，请参阅[CREATE XML INDEX](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)。  
  
## <a name="remarks"></a>注释  
 对于基表中的每个 XML 列，可能有多个辅助选择性 XML 索引。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 XML 列中必须存在选择性 XML 索引，然后才能对该列创建辅助选择性 XML 索引。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求对表或视图具有 ALTER 权限。 用户必须是 **sysadmin** 固定服务器角色的成员，或者是 **db_ddladmin** 和 **db_owner** 固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例对路径 `pathabc`创建辅助选择性 XML 索引。 索引的路径是从分配的名称[CREATE SELECTIVE XML INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR ( pathabc );  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择性 XML 索引 (SXI)](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [创建、更改和删除辅助选择性 XML 索引](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)  
  
  

