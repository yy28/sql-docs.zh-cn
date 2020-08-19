---
description: sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
title: sp_fulltext_semantic_register_language_statistics_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7bca458ae688762c45d365a2d65b92106288952a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486026"
---
# <a name="sp_fulltext_semantic_register_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例中注册预先填充的语义语言统计数据库。  
  
 仅在已附加此语言统计数据库并使用此存储过程注册该数据库后，才能启动语义提取。 只需对每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例执行一次此任务。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] 'database_name';  
GO  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 参数  
 [ @dbname =] "*database_name*"  
 要为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例注册的语义语言统计数据库的名称。 必须已经附加数据库。 *database_name* **sysname**，并且不能为 NULL。  
  
## <a name="return-code-value"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="result-set"></a>结果集  
 无。  
  
## <a name="general-remarks"></a>一般备注  
 语义语言统计数据库包含对文本内容进行语义处理时所需的与语言相关的统计信息。  
  
 **sp_fulltext_semantic_register_language_statistics_db** 执行以下步骤：  
  
1.  检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的版本是否支持语义处理。  
  
2.  检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是否尚未定义语义语言统计数据库。  
  
3.  检查该数据库是否是有效的语义语言统计数据库。  
  
4.  对语义语言统计数据库设置权限，以限制用户访问该数据库。  
  
5.  插入为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例定义语义语言统计数据库的名称的元数据。  
  
6.  插入定义已安装的语义语言统计数据库与内部语言模型表之间的映射的元数据。  
  
7.  检查以确保该数据库可供使用。  
  
 有关详细信息，请参阅 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>Metadata  
 有关实例上安装的语义语言统计信息数据库的信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请查询目录视图 [fulltext_semantic_language_statistics_database Sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要具有 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何通过调用 **sp_fulltext_semantic_register_language_statistics_db**来注册语义语言统计信息数据库。  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
