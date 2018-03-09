---
title: sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 697af637dc9721fa7f8777f038c6ba3717ce2c2b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spfulltextsemanticunregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例中撤消注册现有语义语言统计数据库并删除所有关联元数据。  
  
 此语句不分离数据库，也不会从文件系统中删除物理数据库文件。 撤消注册该数据库后，您可以分离该数据库并删除物理数据库文件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="Arguments"></a> 参数  
 此过程不需要任何参数。 由于一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例仅有一个语义语言统计数据库，所以不必标识该数据库。  
  
## <a name="return-code-value"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-set"></a>结果集  
 无。  
  
## <a name="general-remarks"></a>一般备注  
 撤消注册语义语言统计数据库后，与之关联的所有元数据也随之删除。  
  
 **sp_fulltext_semantic_unregister_language_statistics_db**执行以下步骤：  
  
1.  确保当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例未在进行语义填充。  
  
2.  删除与指定的语义语言统计数据库关联的所有元数据。  
  
 有关详细信息，请参阅 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关安装的实例上的语义语言统计数据库信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，查询目录视图[sys.fulltext_semantic_language_statistics_database &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 需要具有 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何通过调用取消注册语义语言统计数据库**sp_fulltext_semantic_unregister_language_statistics_db**。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
