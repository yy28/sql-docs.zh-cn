---
title: "sys.sp_rda_set_query_mode (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a98d67b6d6cec581cdfcff31f7f9c0fd692b2520
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定针对当前已启用延伸的数据库和其表的查询返回本地和远程数据 （默认值） 或仅限本地数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>参数  
 [ @mode = ] *@mode*  
 是以下值之一。  
  
-   **已禁用**针对已启用延伸的表的所有查询都失败。  
  
-   **LOCAL_ONLY**针对已启用延伸的表的查询返回仅限本地数据。  
  
-   **LOCAL_AND_REMOTE**针对已启用延伸的表的查询返回本地和远程数据。 这是默认行为。  
  
 [ @force = ]  *@force*  
 是一个可选的位值，你可以设置为 1，如果你想要更改查询模式，而不进行验证。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>注释  
 以下扩展存储的过程还设置已启用延伸的数据库的查询模式。  
  
-   **sp_rda_deauthorize_db**  
  
     运行之后**sp_rda_deauthorize_db** ，对已启用延伸的数据库和表的所有查询都失败。 也就是说，查询模式设置为已禁用。 若要退出此模式，请执行以下操作之一。  
  
    -   运行[sys.sp_rda_reauthorize_db &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新连接到远程 Azure 数据库。 此操作会自动重置为查询模式 LOCAL_AND_REMOTE，它是 Stretch Database 的默认行为。 也就是说，查询返回结果从本地和远程数据。  
  
    -   运行[sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)具有 LOCAL_ONLY 自变量，以便继续针对仅限本地数据运行查询。  
  
-   **sp_rda_reauthorize_db**  
  
     当你运行[sys.sp_rda_reauthorize_db &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新连接到远程 Azure 数据库，此操作会自动重置的查询模式 LOCAL_AND_REMOTE，到它是 Stretch Database 的默认行为。 也就是说，查询返回结果从本地和远程数据。  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_rda_deauthorize_db &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
