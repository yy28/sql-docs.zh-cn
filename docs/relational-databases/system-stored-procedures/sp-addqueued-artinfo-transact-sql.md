---
title: sp_addqueued_artinfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 33769260b25ef3f6127f6f12ac54af07c5951ad1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820662"
---
# <a name="sp_addqueued_artinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  应使用[sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)过程，而不是**sp_addqueued_artinfo**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)生成包含**sp_addqueued_artinfo**和**sp_addsynctrigger**调用的脚本。  
  
 在订阅服务器上创建用于跟踪项目订阅信息（排队更新和立即更新，并将排队更新作为故障转移）的[MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)表。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addqueued_artinfo [ @artid= ] 'artid'  
        , [ @article= ] 'article'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @dest_table= ] 'dest_table'  
        , [ @owner = ] 'owner'  
        , [ @cft_table= ] 'cft_table'  
```  
  
## <a name="arguments"></a>参数  
`[ @artid = ] 'artid'`项目 ID 的名称。 *artid*的值为**int**，无默认值  
  
`[ @article = ] 'article'`要编写脚本的项目的名称。 *项目*的**sysname**，无默认值  
  
`[ @publisher = ] 'publisher'`发布服务器的名称。 *发布服务器*的**sysname**，无默认值。  
  
`[ @publisher_db = ] 'publisher_db'`发布服务器数据库的名称。 *publisher_db* **sysname**，无默认值。  
  
`[ @publication = ] 'publication'`要编写脚本的发布的名称。 *发布*为**sysname**，无默认值。  
  
`[ @dest_table = ] _'dest_table'`目标表的名称。 *dest_table* **sysname**，无默认值。  
  
 [** @owner =** ] **"**_owner_**"**  
 订阅的所有者。 *所有者*为**sysname**，无默认值。  
  
`[ @cft_table = ] 'cft_table'`本文的排队更新冲突表的名称。 *cft_table* **sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addqueued_artinfo**由分发代理作为订阅初始化的一部分使用。 此存储过程通常不能由用户运行，但如果用户需要手动设置订阅，则此过程很有用。  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) ，而不是**sp_addqueued_artinfo**。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员或**db_owner**固定数据库角色的成员才能执行**sp_addqueued_artinfo**。  
  
## <a name="see-also"></a>另请参阅  
 [事务复制的可更新订阅](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact-sql&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
