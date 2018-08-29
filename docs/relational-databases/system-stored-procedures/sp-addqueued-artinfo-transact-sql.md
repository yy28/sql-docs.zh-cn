---
title: sp_addqueued_artinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e6ee6f6be9aa7887fc323ab7ba392c4e1c1dbd3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021846"
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)过程应使用而不是**sp_addqueued_artinfo**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)生成包含一个脚本**sp_addqueued_artinfo**并**sp_addsynctrigger**调用。  
  
 创建[MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)表在订阅服务器用来跟踪项目订阅信息 （排队更新和排队更新作为故障转移的立即更新）。 此存储过程在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@artid=** ] **'***artid*****  
 项目 ID 的名称。 *artid*是**int**，无默认值  
  
 [  **@article=**] **'***文章*****  
 要写入脚本的项目的名称。 *文章*是**sysname**，无默认值  
  
 [ **@publisher=**] **'***publisher***'**  
 是发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication=**] **'***publication***'**  
 要写入脚本的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@dest_table=** ] *' dest_table * * ***  
 目标表的名称。 *dest_table*是**sysname**，无默认值。  
  
 [ **@owner =** ] **'***所有者*****  
 是订阅的所有者。 *所有者*是**sysname**，无默认值。  
  
 [  **@cft_table=** ] **'***cft_table*****  
 针对该项目的已排队的更新冲突表的名称。 *cft_table*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_addqueued_artinfo**由分发代理作为订阅初始化的一部分。 此存储过程通常不能由用户运行，但如果用户需要手动设置订阅，则此过程很有用。  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)而不是**sp_addqueued_artinfo**。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addqueued_artinfo**。  
  
## <a name="see-also"></a>请参阅  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact SQL&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
