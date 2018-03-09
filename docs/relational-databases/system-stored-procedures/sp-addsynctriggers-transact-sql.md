---
title: "sp_addsynctriggers (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf7770a9388c18922aeb551246c314caba5860fe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spaddsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在订阅服务器上创建与所有类型的可更新订阅（立即、排队和将排队更新作为故障转移的立即更新）一起使用的触发器。 此存储过程在订阅服务器的订阅数据库中执行。  
  
> [!IMPORTANT]  
>  [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)过程应使用而不是**sp_addsynctrigger**。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)生成脚本，其中包含**sp_addsynctrigger**调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>参数  
 [  **@sub_table=**] *sub_table*  
 订阅服务器表的名称。 *sub_table*是**sysname**，无默认值。  
  
 [  **@sub_table_owner=**] *sub_table_owner*  
 订阅服务器表的所有者名称。 *sub_table_owner*是**sysname**，无默认值。  
  
 [  **@publisher=**] *发布服务器*  
 是发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=**] *publisher_db*  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，无默认值。 如果为 NULL，则使用当前数据库。  
  
 [  **@publication=**] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@ins_proc=**] *ins_proc*  
 在发布服务器上支持同步事务插入的存储过程的名称。 *ins_proc*是**sysname**，无默认值。  
  
 [  **@upd_proc=**] *upd_proc*  
 在发布服务器上支持同步事务更新的存储过程的名称。 *ins_proc*是**sysname**，无默认值。  
  
 [  **@del_proc=**] *del_proc*  
 在发布服务器上支持同步事务删除的存储过程的名称。 *ins_proc*是**sysname**，无默认值。  
  
 [  **@cftproc =** ] *cftproc*  
 允许排队更新的发布使用的自动生成过程的名称。 *cftproc*是**sysname**，无默认值。 对于允许立即更新的发布，该值为 NULL。 此参数应用于允许排队更新（排队更新和将排队更新作为故障转移的立即更新）的发布。  
  
 [  **@proc_owner =** ] *proc_owner*  
 指定发布服务器中的用户帐户，在该帐户下创建了用于更新发布（排队和/或立即）的所有自动生成存储过程。 *proc_owner*是**sysname**无默认值。  
  
 [  **@identity_col=**] *identity_col*  
 发布服务器上标识列的名称。 *identity_col*是**sysname**，默认值为 NULL。  
  
 [  **@ts_col=**] *timestamp_col*  
 是的名称**时间戳**发布服务器上的列。 *timestamp_col*是**sysname**，默认值为 NULL。  
  
 [  **@filter_clause=**] *filter_clause*  
 是定义水平筛选器的限制 (WHERE) 子句。 当输入限制子句时，将省略关键字 WHERE。 *filter_clause*是**nvarchar （4000)**，默认值为 NULL。  
  
 [  **@primary_key_bitmap =**] *primary_key_bitmap*  
 表内主键列的位图。 *primary_key_bitmap*是**varbinary(4000)**，无默认值。  
  
 [  **@identity_support =** ] *identity_support*  
 使用排队更新时启用和禁用自动标识范围处理。 *identity_support*是**位**，默认值为**0**。 **0**意味着没有任何标识范围支持， **1**启用自动标识范围处理。  
  
 [  **@independent_agent =** ] *independent_agent*  
 指示只有一个用于该发布的分发代理（独立代理），还是每个发布数据库和订阅数据库对都有一个分发代理（共享代理）。 该值反映了发布服务器上所定义发布的 independent_agent 属性值。 *independent_agent*有一点默认值为**0**。 如果**0**，代理是共享代理。 如果**1**，代理是独立的代理。  
  
 [  **@distributor =** ] *分发服务器*  
 是分发服务器的名称。 *分发服务器*是**sysname**，无默认值。  
  
 [  **@pubversion** =] *pubversion*  
 指示发布服务器的版本。 *pubversion*是**int**，默认值为 1。 **1**意味着，发布服务器版本是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 或更早版本;**2**意味着，发布服务器是[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 3 (SP3) 或更高版本。 *pubversion*必须显式设置为**2**发布服务器的版本时[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]SP3 或更高版本。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addsynctriggers**由分发代理将它用作订阅初始化的一部分。 此存储过程通常不能由用户运行，但如果用户需要手动设置非同步订阅，则此过程很有用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addsynctriggers**。  
  
## <a name="see-also"></a>另请参阅  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
