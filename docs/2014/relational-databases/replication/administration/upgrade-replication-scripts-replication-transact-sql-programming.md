---
title: 升级复制脚本（复制 Transact-SQL 编程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server replication], upgrading
- upgrading SQL Server, replicated databases
- upgrading replication applications
- replication [SQL Server], scripting
- replication [SQL Server], upgrading
- upgrading replicated databases
ms.assetid: 0b8720bd-f339-4842-bc8f-b35a46f6d3ee
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bd13dfcbb5c90cc74d2e135f65eee8d3b4bf8393
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294757"
---
# <a name="upgrade-replication-scripts-replication-transact-sql-programming"></a>升级复制脚本（复制 Transact-SQL 编程）
  [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本文件可用于以编程方式配置复制拓扑。 有关详细信息，请参阅[复制系统存储过程概念](../concepts/replication-system-stored-procedures-concepts.md)。  
  
> [!IMPORTANT]  
>  虽然不需要升级由 `sysadmin` 角色的成员执行的脚本，我们仍建议您按照本主题中的说明修改现有脚本。 按照 [Replication Agent Security Model](../security/replication-agent-security-model.md)主题的“代理所需权限”部分的说明为每个复制代理指定一个具有最低权限的帐户。  
  
 这些安全改进允许您显式指定用于执行复制代理作业的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帐户，从而可对权限进行更多控制，这些安全改进会影响现有脚本中的以下存储过程：  
  
-   **sp_addpublication_snapshot**：  
  
     现在，执行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) 来创建用于在分发服务器上运行快照代理的作业时，应提供 Windows 凭据作为 **@job_login** 和 **@job_password**。  
  
-   **sp_addpushsubscription_agent**：  
  
     现在应执行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql) 来显式添加作业，并提供用于在分发服务器上运行分发代理作业的 Windows 凭据（**@job_login** 和 **@job_password**）。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，当创建推送订阅时会自动执行此操作。  
  
-   **sp_addmergepushsubscription_agent**：  
  
     现在应执行 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql) 来显式添加作业，并提供用于在分发服务器上运行合并代理作业的 Windows 凭据（**@job_login** 和 **@job_password**）。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，当创建推送订阅时会自动执行此操作。  
  
-   **sp_addpullsubscription_agent**：  
  
     现在，执行 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) 来创建用于在订阅服务器上运行分发代理的作业时，应提供 Windows 凭据作为 **@job_login** 和 **@job_password**。  
  
-   **sp_addmergepullsubscription_agent**：  
  
     现在，执行 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) 来创建用于在订阅服务器上运行合并代理的作业时，应提供 Windows 凭据作为 **@job_login** 和 **@job_password**。  
  
-   **sp_addlogreader_agent**：  
  
     现在应执行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) 来手动添加作业，并提供用于在分发服务器上运行日志读取器代理的 Windows 凭据。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，当创建事务发布时会自动执行此操作。  
  
-   **sp_addqreader_agent**：  
  
     现在应执行 [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql) 来手动添加作业，并提供用于在分发服务器上运行队列读取器代理的 Windows 凭据。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，当创建支持排队更新的事务发布时会自动执行此操作。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]引入的安全模式中，复制代理总是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @job_name **@job_name** @job_login **@job_password**。 有关运行复制代理作业时所使用的 Windows 帐户的要求，请参阅 [Replication Agent Security Model](../security/replication-agent-security-model.md)。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果将凭据保存在脚本文件中，请确保该文件本身受到安全保护。  
  
### <a name="to-upgrade-scripts-that-configure-a-snapshot-or-transactional-publication"></a>升级用于配置快照发布或事务发布的脚本  
  
1.  在现有脚本中的 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 前面，针对发布服务器上的发布数据库执行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql)。 为 **@job_name** @job_login **@job_password**。 如果代理在连接到发布服务器时将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证，则还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** ，并为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**。 这样，便为发布数据库创建了一个日志读取器代理作业。  
  
    > [!NOTE]  
    >  此步骤仅针对事务发布，无需对快照发布执行该步骤。  
  
2.  （可选）在 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 前面，针对分发服务器上的分发数据库执行 [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql)。 为 **@job_name** @job_login **@job_password**。 这样，便为分发服务器创建了一个队列读取器代理作业。  
  
    > [!NOTE]  
    >  仅需要对支持排队更新订阅服务器的事务发布执行此步骤。  
  
3.  （可选）更新 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 的执行，以便对用于实现新复制功能的参数设置任何非默认的值。  
  
4.  在 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) 后面，针对发布服务器上的发布数据库执行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 指定 **@publication** ，并为 **@job_name** @job_login **@job_password**。 如果代理在连接到发布服务器时将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证，则还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** ，并为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**。 此操作将为发布创建一个快照代理作业。  
  
5.  （可选）更新 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 的执行，以便对用于实现新复制功能的参数设置任何非默认的值。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-snapshot-or-transactional-publication"></a>升级向快照发布或事务发布添加订阅的脚本  
  
1.  在执行用于创建订阅的存储过程之后，请确保执行用于创建分发代理作业的存储过程以同步订阅。 所用的存储过程将取决于订阅类型。  
  
    -   对于请求订阅，请更新 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) 的执行，为 **@job_name** 和 **@job_password** 提供用于在订阅服务器上运行分发代理的 Windows 凭据。 此操作将在执行 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)后完成。 有关详细信息，请参阅 [创建请求订阅](../create-a-pull-subscription.md)。  
  
    -   对于推送订阅，请在发布服务器上执行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)。 指定 **@subscriber**、 **@subscriber_db**、 **@publication**，并为 **@job_name** @job_login **@job_password**指定在分发服务器上运行分发代理所使用的 Windows 凭据，同时指定此代理作业的计划。 有关详细信息，请参阅 [Specify Synchronization Schedules](../specify-synchronization-schedules.md)。 此操作将在执行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)后完成。 有关详细信息，请参阅 [创建推送订阅](../create-a-push-subscription.md)。  
  
### <a name="to-upgrade-scripts-that-configure-a-merge-publication"></a>升级用于配置合并发布的脚本  
  
1.  （可选）在现有脚本中，更新 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 的执行，以便对用于实现新复制功能的参数设置任何非默认的值。  
  
2.  在 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) 后面，针对发布服务器上的发布数据库执行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 指定 **@publication** ，并为 **@job_name** @job_login **@job_password**。 如果代理在连接到发布服务器时将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证，则还必须将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** ，并为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @publisher_login **@publisher_login** @job_login **@publisher_password**。 此操作将为发布创建一个快照代理作业。  
  
3.  （可选）更新 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 的执行，以便对用于实现新复制功能的参数设置任何非默认的值。  
  
### <a name="to-upgrade-scripts-that-add-subscriptions-to-a-merge-publication"></a>升级向合并发布添加订阅的脚本  
  
1.  执行完用于创建订阅的存储过程后，请确保执行用于创建合并代理作业的存储过程以同步订阅。 所用的存储过程将取决于订阅类型。  
  
    -   对于请求订阅，请更新 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) 的执行，为 **@job_name** 和 **@job_password** 提供用于在订阅服务器上运行合并代理的 Windows 凭据。 此操作将在执行 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)后完成。 有关详细信息，请参阅 [创建请求订阅](../create-a-pull-subscription.md)。  
  
    -   对于推送订阅，请在发布服务器上执行 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)。 指定 **@subscriber**、 **@subscriber_db**、 **@publication**，并为 **@job_name** @job_login **@job_password**指定在分发服务器上运行分发代理所使用的 Windows 凭据，同时指定此代理作业的计划。 有关详细信息，请参阅 [Specify Synchronization Schedules](../specify-synchronization-schedules.md)。 此操作将在执行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)后完成。 有关详细信息，请参阅 [创建推送订阅](../create-a-push-subscription.md)。  
  
## <a name="example"></a>示例  
 下面是一个用于创建 Product 表的事务发布的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 脚本示例。 此发布支持以排队更新作为故障转移的立即更新。 为了方便阅读，删除了默认参数。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpub80.sql#sp_createtranpub_nwpreupgrade)]  
  
## <a name="example"></a>示例  
 下面的示例将对上一个用于创建事务发布的脚本进行更新，从而可以在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中成功运行。 此发布支持以排队更新作为故障转移的立即更新。 在此示例中显式声明了新参数的默认值。  
  
> [!NOTE]  
>  Windows 凭据是在运行时使用 **sqlcmd** 脚本变量来提供的。  
  
 [!code-sql[HowTo#sp_createtranpub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpublication.sql#sp_createtranpub_nwpostupgrade)]  
  
## <a name="example"></a>示例  
 下面是一个可创建 Customers 表的合并发布的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 脚本示例。 为了方便阅读，删除了默认参数。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepub80.sql#sp_createmergepub_nwpreupgrade)]  
  
## <a name="example"></a>示例  
 下面的示例将对上一个用于创建合并发布的脚本进行升级，从而可以在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中成功运行。 在此示例中显式声明了新参数的默认值。  
  
> [!NOTE]  
>  Windows 凭据是在运行时使用 **sqlcmd** 脚本变量来提供的。  
  
 [!code-sql[HowTo#sp_createmergepub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepublication.sql#sp_createmergepub_nwpostupgrade)]  
  
## <a name="example"></a>示例  
 下面是一个可创建对事务发布的推送订阅的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 脚本示例。 为了方便阅读，删除了默认参数。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwtranpushsub80.sql#sp_createtranpushsub_nwpreupgrade)]  
  
## <a name="example"></a>示例  
 下面的示例将对上一个用于创建对事务发布的推送订阅的脚本进行升级，从而可在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中成功运行。 在此示例中显式声明了新参数的默认值。  
  
> [!NOTE]  
>  Windows 凭据是在运行时使用 **sqlcmd** 脚本变量来提供的。  
  
 [!code-sql[HowTo#sp_createtranpushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createtranpushsub_nwpostupgrade)]  
  
## <a name="example"></a>示例  
 下面是一个可创建对合并发布的推送订阅的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 脚本示例。 为了方便阅读，删除了默认参数。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>示例  
 下面的示例将对上一个用于创建对合并发布的推送订阅的脚本进行升级，从而可在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中成功运行。 在此示例中显式声明了新参数的默认值。  
  
> [!NOTE]  
>  Windows 凭据是在运行时使用 **sqlcmd** 脚本变量来提供的。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpushsub.sql#sp_createmergepushsub_nwpostupgrade)]  
  
## <a name="example"></a>示例  
 下面是一个可创建事务发布的请求订阅的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 脚本示例。 为了方便阅读，删除了默认参数。  
  
 [!code-sql[HowTo#sp_createmergepushsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepushsub80.sql#sp_createmergepushsub_nwpreupgrade)]  
  
## <a name="example"></a>示例  
 下面的示例将对上一个用于创建对事务发布的请求订阅的脚本进行升级，从而可在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中成功运行。 在此示例中显式声明了新参数的默认值。  
  
> [!NOTE]  
>  Windows 凭据是在运行时使用 **sqlcmd** 脚本变量来提供的。  
  
 [!code-sql[HowTo#sp_createtranpullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createtranpullsub_nwpostupgrade)]  
  
## <a name="example"></a>示例  
 下面是一个可创建对合并发布的请求订阅的 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 脚本示例。 为了方便阅读，删除了默认参数。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpreupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwmergepullsub80.sql#sp_createmergepullsub_nwpreupgrade)]  
  
## <a name="example"></a>示例  
 下面的示例将对上一个用于创建对合并发布的请求订阅的脚本进行升级，从而可在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中成功运行。 在此示例中显式声明了新参数的默认值。  
  
> [!NOTE]  
>  Windows 凭据是在运行时使用 **sqlcmd** 脚本变量来提供的。  
  
 [!code-sql[HowTo#sp_createmergepullsub_NWpostupgrade](../../../snippets/tsql/SQL15/replication/howto/tsql/createnwpullsub.sql#sp_createmergepullsub_nwpostupgrade)]  
  
## <a name="see-also"></a>请参阅  
 [Create a Publication](../publish/create-a-publication.md)   
 [Create a Push Subscription](../create-a-push-subscription.md)   
 [Create a Pull Subscription](../create-a-pull-subscription.md)   
 [查看和修改复制安全设置](../security/view-and-modify-replication-security-settings.md)   
 [MSSQL_ENG021797](../mssql-eng021797.md)   
 [MSSQL_ENG021798](../mssql-eng021798.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [升级复制的数据库](../../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
