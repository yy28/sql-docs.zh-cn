---
title: "CREATE FULLTEXT CATALOG (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CATALOG_TSQL
- CREATE_FULLTEXT_TSQL
- FULLTEXT_TSQL
- FULLTEXT CATALOG
- CREATE FULLTEXT CATALOG
- CREATE_FULLTEXT_CATALOG_TSQL
- CATALOG
- FULLTEXT_CATALOG_TSQL
- CREATE FULLTEXT
- FULLTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- CREATE FULLTEXT CATALOG statement
ms.assetid: d7a8bd93-e2d7-4a40-82ef-39069e65523b
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: f08bdaeaacb970c839ea1d7bb31c44f454daadf8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="create-fulltext-catalog-transact-sql"></a>CREATE FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为数据库创建全文目录。 一个全文目录可以包含多个全文索引，但一个全文索引只能用于构成一个全文目录。 每个数据库可以不包含全文目录或包含多个全文目录。  
  
 无法创建全文目录中的**master**，**模型**，或**tempdb**数据库。  
  
> [!IMPORTANT]  
>  从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，全文目录为虚拟对象且不再属于任何文件组。 全文目录是表示一组全文索引的逻辑概念。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE FULLTEXT CATALOG catalog_name  
     [ON FILEGROUP filegroup ]  
     [IN PATH 'rootpath']  
     [WITH <catalog_option>]  
     [AS DEFAULT]  
     [AUTHORIZATION owner_name ]  
  
<catalog_option>::=  
     ACCENT_SENSITIVITY = {ON|OFF}  
  
```  
  
## <a name="arguments"></a>参数  
 *catalog_name*  
 新目录的名称。 在当前数据库的所有目录名中，该目录名必须唯一。 与全文目录对应的文件名（请参阅 ON FILEGROUP）在数据库的所有文件中也必须唯一。 如果该目录名已用于数据库中的其他目录，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将返回错误。  
  
 目录名的长度不能超过 120 个字符。  
  
 ON FILEGROUP *filegroup*  
 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，此子句没有任何作用。  
  
 在路径中*rootpath*  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，此子句没有任何作用。  
  
 ACCENT_SENSITIVITY = {ON|OFF}  
 指定该目录的全文索引是否区分重音。 在更改此属性后，必须重新生成索引。 默认情况下，将使用数据库排序规则中所指定的区分重音设置。 若要显示的数据库排序规则，请使用**sys.databases**目录视图。  
  
 若要确定的全文目录的当前区分重音属性设置，请使用具有的 FULLTEXTCATALOGPROPERTY 函数**accentsensitivity**针对的属性值*catalog_name*。 如果返回值为“1”，则全文目录区分重音；如果该值为“0”，则该目录不区分重音。  
  
 AS DEFAULT  
 指定该目录为默认目录。 如果在未显式指定全文目录的情况下创建全文索引，则将使用默认目录。 如果现有全文目录已标记为 AS DEFAULT，则将新目录设置为 AS DEFAULT 将使该目录成为默认全文目录。  
  
 授权*owner_name*  
 将全文目录的所有者设置为数据库用户名或角色的名称。 如果*owner_name*是一种角色、 角色必须是当前用户是的成员的角色的名称或运行该语句的用户必须是数据库所有者或系统管理员联系。  
  
 如果*owner_name*是用户名称，用户名称必须是以下项之一：  
  
-   运行语句的用户的名称。  
  
-   执行命令的用户拥有其模拟权限的用户的名称。  
  
-   或者，执行命令的用户必须是数据库所有者或系统管理员。  
  
 *owner_name*还必须授予对指定的全文目录的 TAKE OWNERSHIP 权限。  
  
## <a name="remarks"></a>注释  
 全文目录 ID 从 00005 开始，每创建一个新目录，ID 值就会递增 1。  
  
## <a name="permissions"></a>Permissions  
 用户必须在数据库中，具有 CREATE FULLTEXT CATALOG 权限，或者是属于**db_owner**，或**db_ddladmin**固定数据库角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例将创建一个全文目录和一个全文索引。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume) KEY INDEX PK_JobCandidate_JobCandidateID;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.fulltext_catalogs &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact SQL &#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)   
 
  
  

