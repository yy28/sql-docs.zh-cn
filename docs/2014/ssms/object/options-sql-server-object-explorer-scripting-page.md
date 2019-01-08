---
title: 选项 （SQL Server 对象资源管理器-脚本页） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81e4bafbd596894a8cecbeb707a5d8be698c1f3b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764399"
---
# <a name="options-sql-server-object-explorer-scripting-page"></a>选项 （SQL Server 对象资源管理器-脚本页）
  使用此页可设置脚本选项，以应用于**对象资源管理器**中对象上下文菜单上的以下命令：  
  
-   用于用户表和视图的“编辑”命令。  
  
-   **脚本\<对象 > 作为**用于用户创建对象的命令。  
  
-   用于用户创建对象的“修改”命令。  
  
-   本页也可用于设置“生成 SQL Server 脚本向导”的脚本选项默认值。  
  
## <a name="remarks"></a>备注  
 **编辑**并**修改**命令可能会产生不同的结果**脚本\<对象 > 作为**命令用于同一选项设置。 “编辑”和“修改”命令用于在查询编辑器会话期间修改当前数据库中的对象。 **脚本\<对象 > 作为**命令用于生成一个脚本，以便它可用于更高版本创建的对象。  
  
## <a name="options"></a>选项  
 通过从每个选项右侧列表中的可用设置中进行选择，可以指定脚本选项。  
  
### <a name="general-scripting-options"></a>常规脚本选项  
 **分隔各条语句**  
 使用批处理分隔符分隔各条 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 若要更改**查询编辑器**，选择“工具”/“选项”/“查询执行”/“SQL Server”/“常规”/“批处理分隔符”。 默认值为 False。 有关详细信息，请参阅[GO &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/sql-server-utilities-statements-go)。  
  
 **包含说明性标头**  
 通过将每个对象的脚本分隔为多个部分以向脚本添加说明性注释。 默认值为 True。 有关详细信息，请参阅[注释&#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/comment-transact-sql)。  
  
 **包含 vardecimal 选项**  
 包含 vardecimal 存储选项。 默认值为 False。 有关详细信息，请参阅并[sp_db_vardecimal_storage_format &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql)。  
  
 **编写更改跟踪的脚本**  
 将更改跟踪信息包含到脚本中。  
  
 **为服务器版本编写脚本**  
 创建可在选定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本上运行的脚本。 无法为早期版本编写 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 新增功能的脚本。 某些为 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 创建的脚本无法在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早期版本的服务器或具有早期 [数据库兼容级别设置](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)的数据库中运行。  
  
 **编写全文目录脚本**  
 包含用于全文目录的脚本。 默认值为 False。 有关详细信息，请参阅[CREATE FULLTEXT CATALOG &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)。  
  
 **脚本使用\<数据库 >**  
 将 USE DATABASE 语句添加到脚本，可在当前 **对象资源管理器** 数据库的上下文中创建数据库对象。 如果希望该脚本可在其他数据库中使用，请选择 False 以忽略该选项。 默认值为 True。 有关详细信息，请参阅 [USE (Transact-SQL)](/sql/t-sql/language-elements/use-transact-sql)。  
  
### <a name="object-scripting-options"></a>对象脚本选项  
 **生成依赖对象的脚本**  
 为在执行所选对象的脚本时需要的附加对象生成脚本。 默认值为 False。  
  
 **包含 If NOT EXISTS 子句**  
 包含一条语句以用来检查在尝试创建各对象之前数据库中不存在该对象。 默认值为 False。 有关详细信息，请参阅[IF...其他&#40;TRANSACT-SQL&#41; ](/sql/t-sql/language-elements/if-else-transact-sql)并[EXISTS &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/exists-transact-sql)。  
  
 **架构限定对象名称**  
 使用对象架构限定对象名称。 默认值为 False。 有关详细信息，请参阅 [创建数据库架构](../../relational-databases/security/authentication-access/create-a-database-schema.md)。  
  
 **编写扩展属性脚本**  
 如果对象具有扩展属性，则在脚本中包含扩展属性。 默认值为 False。 有关详细信息，请参阅 [sp_addextendedproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql)。  
  
 **编写所有者脚本**  
 在生成的脚本中包含所有者。 默认值为 False。  
  
 **编写权限脚本**  
 在脚本中包括数据库对象的权限。 默认值为 True。 有关详细信息，请参阅[权限&#40;数据库引擎&#41;](../../relational-databases/security/permissions-database-engine.md)。  
  
### <a name="tableview-options"></a>表/视图选项  
 以下选项仅应用于表或视图的脚本。  
  
 **将用户定义数据类型转换为基类型**  
 将用户定义数据类型转换为用于创建此用户定义数据类型的基类型。 将运行脚本的数据库中不存在源数据库用户定义数据类型时，请使用 True。 使用 False 可以保留用户定义数据类型。 默认值为 False。 有关详细信息，请参阅[CREATE TYPE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)。  
  
 **生成 SET ANSI PADDING 命令**  
 将 SET ANSI_PADDING 语句添加在每条 CREATE TABLE 语句的前后。 默认值为 True。 有关详细信息，请参阅 [SET ANSI_PADDING (Transact-SQL)](/sql/t-sql/statements/set-ansi-padding-transact-sql)。  
  
 **包含排序规则**  
 在列定义中包含排序规则。 默认值为 True。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
 **包含 IDENTITY 属性**  
 包含 IDENTITY 种子和 IDENTITY 增量的定义。 默认值为 True。 有关详细信息，请参阅 [IDENTITY（属性）&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)。  
  
 **架构限定外键引用**  
 将架构名称添加到 FOREIGN KEY 约束的表引用。 默认值为 True。  
  
 **绑定到脚本的默认值和规则**  
 包括 **sp_bindefault** 和 **sp_bindrule** 绑定存储过程调用。 默认值为 True。 有关详细信息，请参阅[sp_bindefault &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql)并[sp_bindrule &#40;-&#41;](/sql/relational-databases/system-stored-procedures/sp-bindrule-transact-sql)。  
  
 **编写检查约束脚本**  
 将 [CHECK 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 添加到脚本中。 默认值为 True。  
  
 **编写默认值脚本**  
 在脚本中包含列默认值。 默认值为 False。 有关详细信息，请参阅 [CREATE DEFAULT (Transact-SQL)](/sql/t-sql/statements/create-default-transact-sql)。  
  
 **编写文件组脚本**  
 在 ON 子句中为表定义指定文件组。 默认值为 False。 有关详细信息，请参阅 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)。  
  
 **编写外键脚本**  
 在脚本中包含 [FOREIGN KEY 约束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 。 默认值为 False。  
  
 **编写全文检索脚本**  
 在脚本中包含全文检索。 默认值为 False。 有关详细信息，请参阅[CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)。  
  
 **编写索引脚本**  
 在脚本中包含聚集索引、非聚集索引和 XML 索引。 默认值为 True。 有关详细信息，请参阅 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)。  
  
 **编写分区方案脚本**  
 在脚本中包含表分区方案。 默认值为 False。 有关详细信息，请参阅[CREATE PARTITION SCHEME &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-partition-scheme-transact-sql)。  
  
 **编写主键脚本**  
 在脚本中包含 [和 FOREIGN KEY 约束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 。 默认值为 True。  
  
 **编写统计信息脚本**  
 在脚本中包含用户定义统计信息。 默认值为 False。 有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **编写触发器脚本**  
 在脚本中包含触发器。 默认值为 False。 有关详细信息，请参阅 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)。  
  
 **编写唯一键脚本**  
 在脚本中包含 [UNIQUE 约束和 CHECK 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 。 默认值为 False。  
  
 **编写视图列脚本**  
 在视图页眉中声明视图列。 默认值为 False。 有关详细信息，请参阅 [CREATE VIEW (Transact-SQL)](/sql/t-sql/statements/create-view-transact-sql)。  
  
 **ScriptDriIncludeSystemNames**  
 包含系统生成的约束名称，以强制声明性引用完整性。 默认值为 False。 有关详细信息，请参阅[REFERENTIAL_CONSTRAINTS &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-information-schema-views/referential-constraints-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [生成脚本 (SQL Server Management Studio)](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)  
  
  
