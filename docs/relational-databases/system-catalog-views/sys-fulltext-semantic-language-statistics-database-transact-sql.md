---
title: sys. fulltext_semantic_language_statistics_database （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 0decfac8cf28727a3ba3f4bf5ad54e8f9ff8bee9
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902177"
---
# <a name="sysfulltext_semantic_language_statistics_database-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  返回有关在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例上安装的语义语言统计数据库的行。  
  
 通过查询此视图，您可以查找语义处理所需的语义语言统计组件。  
   
  
||||  
|-|-|-|  
|**列名**|**Type**|**说明**|  
|**database_id**|**int**|数据库 ID（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中唯一）。|  
|**register_date**|**datetime**|注册数据库进行语义处理的日期。|  
|**registered_by**|**int**|注册数据库进行语义处理的服务器主体的 ID。|  
|**version**|**nvarchar(128)**|针对语义语言统计数据库的最新版本信息。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关语义索引支持的语言的信息，请查询目录视图[sys.databases &#40;transact-sql&#41;fulltext_semantic_languages ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何查询**fulltext_semantic_language_statistics_database sys.databases**以获取有关在的当前实例上注册的语义语言统计数据库 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的信息。  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
