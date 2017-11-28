---
title: "ALTER FULLTEXT CATALOG (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FULLEXT_CATALOG_TSQL
- ALTER FULLEXT CATALOG
dev_langs: TSQL
helpviewer_keywords:
- modifying full-text catalogs
- full-text catalogs [SQL Server], rebuilding
- accent sensitivity
- ALTER FULLTEXT CATALOG statement
- full-text catalogs [SQL Server], modifying
- full-text catalogs [SQL Server], reorganizing
ms.assetid: 31a47aaf-6c7f-48a4-a86a-d57aec66c9cb
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa56a980fa5c5c74a1868f4c03ec791175022f76
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-fulltext-catalog-transact-sql"></a>ALTER FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  更改全文目录的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER FULLTEXT CATALOG catalog_name   
{ REBUILD [ WITH ACCENT_SENSITIVITY = { ON | OFF } ]  
| REORGANIZE  
| AS DEFAULT   
}  
```  
  
## <a name="arguments"></a>参数  
 *catalog_name*  
 指定要修改的目录的名称。 如果不存在具有指定名称的目录， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回一个错误并且不会执行 ALTER 操作。  
  
 REBUILD  
 告知 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新生成整个目录。 重新生成目录时，将删除现有目录，并在其原位置创建一个新目录。 具有全文索引引用的所有表都与此新目录相关联。 重新生成会重置数据库系统表中的全文元数据。  
  
 WITH ACCENT_SENSITIVITY = {ON|OFF}  
 指定要更改的全文索引和查询的目录是区分重音的，还是不区分重音的。  
  
 若要确定的全文目录的当前区分重音属性设置，请使用具有的 FULLTEXTCATALOGPROPERTY 函数**accentsensitivity**针对的属性值*catalog_name*。 如果函数返回“1”，则全文目录是区分重音的；如果函数返回“0”，则目录是不区分重音的。  
  
 目录和数据库的默认重音区分设置是相同的。  
  
 REORGANIZE  
 告知[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行*主合并*，涉及到合并为一个大的索引编制索引的过程中创建的较小索引。 合并的全文索引碎片，可以提高性能，并释放磁盘和内存资源。 如果全文目录频繁发生更改，则请定期使用该命令重新组织全文目录。  
  
 REORGANIZE 还可以优化内部索引和目录结构。  
  
 请注意，根据索引数据的数量，完成主合并操作可能要花费一些时间。 对大量数据进行主合并会创建一个长时间运行的事务，在检查点期间延迟事务日志的截断。 在这种情况下，事务日志可能会在完整恢复模式下显著增长。 作为最佳实践，在使用完整恢复模式的数据库中重新组织较大的全文索引之前，应确保事务日志中包含足够的空间用于长时间运行的事务。 有关详细信息，请参阅 [管理事务日志文件的大小](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)。  
  
 AS DEFAULT  
 指定此目录为默认目录。 如果创建全文索引时没有指定目录，则将使用默认目录。 如果存在默认全文目录，则以 AS DEFAULT 设置该目录将覆盖现有默认设置。  
  
## <a name="permissions"></a>Permissions  
 用户必须具有 ALTER 权限的全文目录，或者是的成员**db_owner**， **db_ddladmin**固定数据库角色或 sysadmin 固定的服务器角色。  
  
> [!NOTE]  
>  若要使用 ALTER FULLTEXT CATALOG AS DEFAULT，用户必须对全文目录具有 ALTER 权限，对数据库具有 CREATE FULLTEXT CATALOG 权限。  
  
## <a name="examples"></a>示例  
 下面的示例更改默认全文目录 `accentsensitivity`（区分重音）的 `ftCatalog` 属性。  
  
```  
--Change to accent insensitive  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog   
REBUILD WITH ACCENT_SENSITIVITY=OFF;  
GO  
-- Check Accentsensitivity  
SELECT FULLTEXTCATALOGPROPERTY('ftCatalog', 'accentsensitivity');  
GO  
--Returned 0, which means the catalog is not accent sensitive.  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.fulltext_catalogs &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [创建 FULLTEXT CATALOG &#40;Transact SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact SQL &#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)  
  
  
