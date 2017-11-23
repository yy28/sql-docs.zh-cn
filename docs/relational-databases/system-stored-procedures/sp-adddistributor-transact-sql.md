---
title: "sp_adddistributor (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bfdf3aa6cbd888385f00afad8594cb6427ac071b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  中创建一个条目[sys.sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md)表 （如果没有一个），将标记为分发服务器，服务器条目，并将存储属性信息。 此存储过程在分发服务器上对主数据库执行以注册服务器，并将其标记为分发服务器。 如果是远程分发服务器，此存储过程还在发布服务器上对主数据库执行以注册远程分发服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@distributor=**] *分发服务器*  
 分发服务器名称。 *分发服务器*是**sysname**，无默认值。 只有在设置远程分发服务器时才使用此参数。 它将添加条目中的分发服务器属性**msdb...MSdistributor**表。  
  
 [  **@heartbeat_interval=**] *heartbeat_interval*  
 是最大的代理可以转而不记录任何进度消息的分钟数。 *heartbeat_interval*是**int**，默认值为 10 分钟。 创建按此间隔运行的 SQL Server 代理作业，以检查正在运行的复制代理的状态。  
  
 [  **@password=**] *密码*]  
 是的密码**distributor_admin**登录名。 *密码*是**sysname**，默认值为 NULL。 如果为 NULL 或空字符串，则密码重置为随机值。 必须在添加第一个远程分发服务器时配置密码。 **distributor_admin**登录名和*密码*为链接的服务器条目用于存储*分发服务器*RPC 连接，包括本地连接。 如果*分发服务器*是本地计算机，密码**distributor_admin**设置为新值。 对于具有远程分发服务器的发布者，相同值*密码*时执行，必须指定**sp_adddistributor**发布服务器和分发服务器。 [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md)可以用于更改分发服务器密码。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@from_scripting=** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 **sp_adddistributor**快照复制、 事务复制和合并复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_adddistributor**。  
  
## <a name="see-also"></a>另请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributor_property &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_dropdistributor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [配置分发](../../relational-databases/replication/configure-distribution.md)  
  
  
