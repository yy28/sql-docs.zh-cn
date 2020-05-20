---
title: sys. sp_rda_set_query_mode （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 06690f79bf2cc708a83ec272906b3f4be09fe03d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807767"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sys. sp_rda_set_query_mode （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定是否对当前启用 Stretch 的数据库及其表进行查询同时返回本地和远程数据（默认值）或本地数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>参数  
 [ @mode =] * \@ 模式*  
 是以下值之一。  
  
-   **已禁用**针对启用 Stretch 的表的所有查询都将失败。  
  
-   **LOCAL_ONLY**针对启用 Stretch 的表的查询仅返回本地数据。  
  
-   **LOCAL_AND_REMOTE**针对启用 Stretch 的表的查询将返回本地和远程数据。 此选项为默认行为。  
  
 [ @force =] * \@ force*  
 如果希望在不验证的情况下更改查询模式，则可以将此值设置为1。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0 （失败）  
  
## <a name="permissions"></a>权限  
 需要 db_owner 权限。  
  
## <a name="remarks"></a>备注  
 以下扩展存储过程还为已启用延伸的数据库设置查询模式。  
  
-   **sp_rda_deauthorize_db**  
  
     运行**sp_rda_deauthorize_db**后，针对已启用延伸的数据库和表的所有查询都将失败。 也就是说，查询模式设置为 "已禁用"。 若要退出此模式，请执行以下操作之一。  
  
    -   运行[sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新连接到远程 Azure 数据库。 此操作会自动将查询模式重置为 LOCAL_AND_REMOTE，这是 Stretch Database 的默认行为。 也就是说，查询从本地和远程数据返回结果。  
  
    -   运行带有 LOCAL_ONLY 参数的 sys.databases，以使查询仅对本地数据运行[sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) 。  
  
-   **sp_rda_reauthorize_db**  
  
     当你运行[sys.databases sp_rda_reauthorize_db &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)重新连接到远程 Azure 数据库时，此操作会自动将查询模式重置为 LOCAL_AND_REMOTE，这是 Stretch Database 的默认行为。 也就是说，查询从本地和远程数据返回结果。  
  
## <a name="see-also"></a>另请参阅  
 [sys. sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
