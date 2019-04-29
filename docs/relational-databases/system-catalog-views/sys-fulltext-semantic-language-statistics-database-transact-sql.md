---
title: sys.fulltext_semantic_language_statistics_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 97631b830acc3babacb5720707722775b4592629
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007531"
---
# <a name="sysfulltextsemanticlanguagestatisticsdatabase-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的当前实例上安装的语义语言统计数据库的行。  
  
 通过查询此视图，您可以查找语义处理所需的语义语言统计组件。  
   
  
||||  
|-|-|-|  
|**列名**|**类型**|**说明**|  
|**database_id**|**int**|数据库 ID（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中唯一）。|  
|**register_date**|**datetime**|注册数据库进行语义处理的日期。|  
|**registered_by**|**int**|注册数据库进行语义处理的服务器主体的 ID。|  
|**version**|**nvarchar(128)**|针对语义语言统计数据库的最新版本信息。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关支持语义索引的语言的信息，请查询目录视图[sys.fulltext_semantic_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何通过查询**sys.fulltext_semantic_language_statistics_database**若要获取有关当前实例上注册的语义语言统计数据库的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [安装和配置语义搜索](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
