---
title: sp_fulltext_semantic_unregister_language_statistics_db （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d6952d245dfc9083c7cfa6e6d36ad991ffd24654
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909140"
---
# <a name="sp_fulltext_semantic_unregister_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例中撤消注册现有语义语言统计数据库并删除所有关联元数据。  
  
 此语句不分离数据库，也不会从文件系统中删除物理数据库文件。 撤消注册该数据库后，您可以分离该数据库并删除物理数据库文件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [transact-sql 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="Arguments"></a> 参数  
 此过程不需要任何参数。 由于一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例仅有一个语义语言统计数据库，所以不必标识该数据库。  
  
## <a name="return-code-value"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-set"></a>结果集  
 无。  
  
## <a name="general-remarks"></a>一般备注  
 撤消注册语义语言统计数据库后，与之关联的所有元数据也随之删除。  
  
 **sp_fulltext_semantic_unregister_language_statistics_db**执行以下步骤：  
  
1.  确保当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例未在进行语义填充。  
  
2.  删除与指定的语义语言统计数据库关联的所有元数据。  

 有关详细信息，请参阅 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>“浏览器”  
 有关在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上安装的语义语言统计信息数据库的信息，请查询目录视图[fulltext_semantic_language_statistics_database &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要具有 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何通过调用**sp_fulltext_semantic_unregister_language_statistics_db**取消注册语义语言统计信息数据库。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
