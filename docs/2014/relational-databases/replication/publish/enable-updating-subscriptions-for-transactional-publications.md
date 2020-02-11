---
title: 对事务发布启用更新订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 963fe86b0d5939c82bffb9c07d5adacbadadba89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68199420"
---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>对事务发布启用更新订阅
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中对事务发布启用更新订阅。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> Security  
 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可以在新建发布向导的 **“发布类型”** 页上对事务发布启用更新订阅。 有关使用此向导的详细信息，请参阅[创建发布](create-a-publication.md)。 不能在创建发布之后启用更新订阅。  
  
 若要使用更新订阅，还必须在新建订阅向导中配置一些选项。 有关详细信息，请参阅 [创建事务发布的可更新订阅](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)。  
  
#### <a name="to-enable-updating-subscriptions"></a>启用更新订阅  
  
1.  在新建发布向导的 **“发布类型”** 页上选择 **“具有可更新订阅的事务发布”**。  
  
2.  在 **“代理安全性”** 页上，除了为快照代理和日志读取器代理指定安全设置外，还要为队列读取器代理指定安全设置。 有关运行队列读取器代理的帐户所需权限的详细信息，请参阅 [Replication Agent Security Model](../security/replication-agent-security-model.md)。  
  
    > [!NOTE]  
    >  即使仅使用即时更新订阅，也要配置队列读取器代理。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 在使用复制存储过程以编程方式创建事务发布时，您可以启用立即或排队更新订阅。  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>创建支持立即更新订阅的发布  
  
1.  如有必要，可为发布数据库创建一个日志读取器代理作业。  
  
    -   如果发布数据库中已经有一个日志读取器代理作业，请继续执行步骤 2。  
  
    -   如果无法确定已发布的数据库是否存在日志读取器代理作业，请在发布服务器上对发布数据库执行 [sp_helplogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql)。 如果结果集为空，则必须创建日志读取器代理作业。  
  
    -   在发布服务器上，执行[&#40;transact-sql&#41;sp_addlogreader_agent ](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)。 指定为[!INCLUDE[msCoName](../../../includes/msconame-md.md)] **@job_name**和**@password**运行代理所用的 Windows 凭据。 如果代理在连接到发布服务器时使用 SQL Server 身份验证，则您还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** 并将 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息指定给 **@publisher_login** 和 **@publisher_password**。  
  
2.  执行 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 并将参数 ****** 的值指定为 @allow_sync_trantrue**。  
  
3.  在发布服务器上，执行[sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 为**@publication**指定在步骤2中使用的发布名称，并为**@job_name**和**@password**运行快照代理所用的 Windows 凭据。 如果代理在连接到发布服务器时使用 SQL Server 身份验证，则您还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** 并将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息指定给 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。  
  
4.  向发布添加项目。 有关详细信息，请参阅 [定义项目](define-an-article.md)。  
  
5.  在订阅服务器上，创建此发布的更新订阅。 有关详细信息，请参阅 [创建事务发布的可更新订阅](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)。  
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>创建支持排队更新订阅的发布  
  
1.  如有必要，可为发布数据库创建一个日志读取器代理作业。  
  
    -   如果发布数据库中已经有一个日志读取器代理作业，请继续执行步骤 2。  
  
    -   如果无法确定已发布的数据库是否存在日志读取器代理作业，请在发布服务器上对发布数据库执行 [sp_helplogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql)。 如果结果集为空，则必须创建一个日志读取器代理作业。  
  
    -   在发布服务器上，执行[&#40;transact-sql&#41;sp_addlogreader_agent ](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)。 指定为**@job_name**和**@password**运行代理所用的 Windows 凭据。 如果代理在连接到发布服务器时使用 SQL Server 身份验证，则您还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** 并将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息指定给 **@publisher_login** 和 **@publisher_password**。  
  
2.  如有必要，可为分发服务器创建一个队列读取器代理作业。  
  
    -   如果分发数据库已经拥有一个队列读取器代理作业，请继续执行步骤 3。  
  
    -   如果您无法确定分发数据库是否已经拥有一个队列读取器代理作业，请在分发服务器上对分发数据库执行 [sp_helpqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql)。 如果结果集为空，则必须创建一个队列读取器代理作业。  
  
    -   在分发服务器上，执行 [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)。 指定为**@job_name**和**@password**运行代理所用的 Windows 凭据。 这些凭据将在队列读取器代理连接到发布服务器和订阅服务器时使用。 有关详细信息，请参阅[复制代理安全模式](../security/replication-agent-security-model.md)。  
  
3.  执行 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)，将参数 ****** 的值指定为 @allow_queued_trantrue** 并将 ****** 的值指定为 **pub wins **、** sub reinit** 或 @conflict_policysub wins**。  
  
4.  在发布服务器上，执行[sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 为**@publication**指定在步骤3中使用的发布名称，并为**@snapshot_job_name**和**@password**运行快照代理所用的 Windows 凭据。 如果代理在连接到发布服务器时使用 SQL Server 身份验证，则您还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** 并将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息指定给 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。  
  
5.  向发布添加项目。 有关详细信息，请参阅 [定义项目](define-an-article.md)。  
  
6.  在订阅服务器上，创建此发布的更新订阅。 有关详细信息，请参阅 [创建事务发布的可更新订阅](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)。  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>为允许排队更新订阅的发布更改冲突策略  
  
1.  在发布服务器上，对发布数据库执行 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 将值 **conflict_policy** 的值指定为 **@property** ，并为 **@conflict_policy**的值指定为 **pub wins**、 **sub reinit** 的值指定为 **@value**中对事务发布启用更新订阅。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例创建一个支持立即和排队更新请求订阅的发布。  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubupdate.sql#sp_createtranupdatingpub)]  
  
## <a name="see-also"></a>另请参阅  
 [设置排队更新冲突解决选项 &#40;SQL Server Management Studio&#41;](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [事务复制的发布类型](../transactional/transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Create a Publication](create-a-publication.md)   
 [创建事务发布的可更新订阅](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [事务复制的可更新订阅](../transactional/updatable-subscriptions-for-transactional-replication.md)   
 [将 sqlcmd 与脚本变量结合使用](../../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
