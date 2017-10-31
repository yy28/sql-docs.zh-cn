---
title: "ALTER INDEX （选择性 XML 索引） |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cca96a8f-7737-42d2-bbcc-03d5f858dcc1
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7854dd1d9365f97628341c4160c368f97308302
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-index-selective-xml-indexes"></a>ALTER INDEX（选择性 XML 索引）
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  修改现有的选择性 XML 索引。 ALTER INDEX 语句更改以下一项或多项：  
  
-   已建立索引的路径的列表（FOR 子句）。  
  
-   命名空间的列表（WITH XMLNAMESPACES 子句）。  
  
-   索引选项（WITH 子句）。  
  
 您不能更改辅助选择性 XML 索引。 有关详细信息，请参阅[Create、 Alter 和 Drop 辅助选择性 XML 索引](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER INDEX index_name  
    ON <table_object>   
    [WITH XMLNAMESPACES ( <xmlnamespace_list> )]  
    FOR ( <promoted_node_path_action_list> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
<promoted_node_path_action_list> ::=   
<promoted_node_path_action_item> [, <promoted_node_path_action_list>]  
  
<promoted_node_path_action_item>::=   
<add_node_path_item_action> | <remove_node_path_item_action>  
  
<add_node_path_item_action> ::=  
ADD <path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<remove_node_path_item_action> ::= REMOVE <path_name>   
  
<path_name_or_typed_node_path>::=   
<path_name> | <typed_node_path>  
  
<typed_node_path> ::=   
<node_path> [[AS XQUERY <xsd_type_ext>] | [AS SQL <sql_type>]]  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | 'node()'  
  
<sql_values_node_path_item> ::=   
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type_ext> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::= character_string_literal  
<xml_namespace_prefix> ::= identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY =OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE =OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> 参数  
 *index_name*  
 要更改的现有索引的名称。  
  
 *\<table_object >*  
 包含要建立索引的 XML 列的表。 使用以下格式之一：  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 [WITH XMLNAMESPACES **(** \<xmlnamespace_list > **)**]  
 要建立索引的路径使用的命名空间的列表。 WITH XMLNAMESPACES 子句的语法的信息，请参阅[WITH XMLNAMESPACES &#40;Transact SQL &#41;](../../t-sql/xml/with-xmlnamespaces.md).  
  
 有关**(** \<promoted_node_path_action_list > **)**  
 要添加或删除的已建立索引的路径的列表。  
  
-   **添加路径。** 添加路径时，您使用的语法与使用 CREATE SELECTIVE XML INDEX 语句创建路径所用的语法相同。 有关可以在 CREATE 或 ALTER 语句中指定的路径的信息，请参阅[指定路径和选择性 XML 索引的优化提示](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)。  
  
-   **删除路径。** 删除路径时，请提供创建路径时的路径名。  
  
 [使用**(** \<index_options > **)**]  
 你只能指定\<index_options > 当你使用 ALTER INDEX 不带 FOR 子句。 在您使用 ALTER INDEX 添加或删除索引中的路径时，索引选项将不是有效的参数。 有关索引选项的信息，请参阅[CREATE XML INDEX &#40;选择性 XML 索引 &#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>注释  
  
> [!IMPORTANT]  
>  在您运行 ALTER INDEX 语句时，始终重新生成选择性 XML 索引。 请务必考虑此过程对服务器资源的影响。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 若要运行 ALTER INDEX，需要对表或视图拥有 ALTER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例说明 ALTER INDEX 语句。 该语句将路径 `'/a/b/m'` 添加到索引的 XQuery 部分，并且从在 [CREATE SELECTIVE XML INDEX (Transact-SQL)](../../t-sql/statements/create-selective-xml-index-transact-sql.md) 主题的示例中创建的索引的 SQL 部分删除路径 `'/a/b/e'`。 要删除的路径由在创建时提供给它的名称标识。  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
);  
```  
  
 下面的示例说明指定索引选项的 ALTER INDEX 语句。 允许索引选项，因为该语句未使用 FOR 子句来添加或删除路径。  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
PAD_INDEX = ON;  
```  
  
## <a name="see-also"></a>另请参阅  
 [选择性 XML 索引 (SXI)](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [创建、 更改和删除选择性 XML 索引](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [为选择性 XML 索引指定路径和优化提示](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  

