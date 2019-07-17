---
title: sys.sp_rda_set_query_mode (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b1450dc8304c2e8d3db5a6fa8b2153f951e70bde
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083604"
---
# <a name="syssprdasetquerymode-transact-sql"></a>sys.sp_rda_set_query_mode (Transact-SQL)
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
 是一个可选的位值，如果你想要更改查询模式，而不进行验证，可以设置为 1。  
  
## <a name="return-code-values"></a>返回代码值  
 0 （成功） 或 > 0 （失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>备注  
 以下扩展存储的过程还设置已启用延伸的数据库的查询模式。  
  
-   **sp_rda_deauthorize_db**  
  
     运行后**sp_rda_deauthorize_db** ，对已启用延伸的数据库和表的所有查询都失败。 也就是说，查询模式设置为禁用。 若要退出此模式，请执行以下操作之一。  
  
    -   运行[sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)以重新连接到远程 Azure 数据库。 此操作会自动重置为查询模式 LOCAL_AND_REMOTE，这是 Stretch Database 的默认行为。 也就是说，查询返回结果从本地和远程数据。  
  
    -   运行[sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)使用 LOCAL_ONLY 自变量，以便继续对本地的数据运行查询。  
  
-   **sp_rda_reauthorize_db**  
  
     在运行时[sys.sp_rda_reauthorize_db &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)若要重新连接到远程 Azure 数据库，此操作会自动重置查询模式 LOCAL_AND_REMOTE，这是默认行为为Stretch Database。 也就是说，查询返回结果从本地和远程数据。  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_rda_deauthorize_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
