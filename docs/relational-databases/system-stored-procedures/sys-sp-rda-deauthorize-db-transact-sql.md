---
title: sys.sp_rda_deauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6ad14f46d0fece2e33fcf9bae5c8c124828bcf2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="syssprdadeauthorizedb-transact-sql"></a>sys.sp_rda_deauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  删除本地已启用延伸的数据库和远程 Azure 数据库之间的经过身份验证的连接。 运行**sp_rda_deauthorize_db**当远程数据库无法访问或处于不一致状态并且你想要更改数据库中的所有已启用延伸的表的查询行为。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>注释  
 运行之后**sp_rda_deauthorize_db** ，对已启用延伸的数据库和表的所有查询都失败。 也就是说，查询模式设置为已禁用。 若要退出此模式，请执行以下操作之一。  
  
-   运行[sys.sp_rda_reauthorize_db &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新连接到远程 Azure 数据库。 此操作会自动重置为查询模式 LOCAL_AND_REMOTE，它是 Stretch Database 的默认行为。 也就是说，查询返回结果从本地和远程数据。  
  
-   运行[sys.sp_rda_set_query_mode &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)具有 LOCAL_ONLY 自变量，以便继续针对仅限本地数据运行查询。  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_rda_set_query_mode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
