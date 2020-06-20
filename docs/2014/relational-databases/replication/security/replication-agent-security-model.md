---
title: 复制代理安全模式 | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da597bf97422f5a0960062b385bc0b67338edfe1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004957"
---
# <a name="replication-agent-security-model"></a>复制代理安全性模式
  可以使用复制代理安全模式，对复制代理运行和建立连接所用的帐户进行精细粒度的控制：可以为每个代理指定不同的帐户。 有关如何指定帐户的详细信息，请参阅[管理复制中的登录名和密码](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)。  
  
> [!IMPORTANT]  
>  **sysadmin** 固定服务器角色的成员配置复制时，可以配置复制代理来模拟 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理帐户。 不指定复制代理的登录名和密码即可完成此操作；但是不推荐这种方法。 作为最佳安全做法，建议以本主题后面的“代理所需权限”部分中介绍的最小权限来为每个代理指定一个帐户。  
  
 和所有可执行文件一样，复制代理在 Windows 帐户的上下文中运行。 它们使用此帐户来建立 Windows 集成安全性连接。 代理在哪个帐户之下运行取决于代理的启动方式：  
  
-   从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理作业启动代理时，默认设置为：使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理作业来启动复制代理时，代理将在配置复制时所指定的帐户的上下文中运行。 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理和复制的详细信息，请参阅本主题后面的“SQL Server 代理下的代理安全性”部分。 有关运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理的帐户所需权限的信息，请参阅[配置 SQL Server 代理](../../../ssms/agent/configure-sql-server-agent.md)。  
  
-   从 MS-DOS 命令行中直接启动或通过脚本启动代理时：代理在通过命令行运行代理的用户帐户的上下文中运行。  
  
-   从使用复制管理对象 (RMO) 或 ActiveX 控件的应用程序启动代理时：代理在调用 RMO 或 ActiveX 控件的应用程序的上下文中运行。  
  
    > [!NOTE]  
    >  不推荐使用 ActiveX 控件。  
  
 建议在 Windows 集成安全性的上下文中建立连接。 为了向后兼容，还可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性。 有关最佳操作的详细信息，请参阅 [Replication Security Best Practices](replication-security-best-practices.md)。  
  
## <a name="permissions-that-are-required-by-agents"></a>代理所需权限  
 用来运行代理并建立连接的帐户需要多种权限。 下表对这些权限进行了说明。 建议每个代理使用不同的 Windows 帐户运行，并应仅授予帐户所需的权限。 有关与多个代理相关的发布访问列表 (PAL) 的信息，请参阅[保护发布服务器](secure-the-publisher.md)。  
  
> [!NOTE]  
>  某些 Windows 操作系统中的用户帐户控制 (UAC) 可防止对快照共享的管理访问。 因此，必须对快照代理、分发代理和合并代理使用的 Windows 帐户显式授予快照共享权限。 即使 Windows 帐户是管理员组的成员，也必须执行此操作。 有关详细信息，请参阅[保护快照文件夹](secure-the-snapshot-folder.md)。  
  
|Agent|权限|  
|-----------|-----------------|  
|快照代理|与分发服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须：<br /><br /> -至少是分发数据库中**db_owner**固定数据库角色的成员。<br /><br /> -对快照共享具有读取、写入和修改权限。<br /><br /> <br /><br /> 用于连接到发布服务器的帐户必须至少是发布数据库中的 **db_owner** 固定数据库角色的成员。|  
|日志读取器代理|与分发服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须至少是分发数据库中的 **db_owner** 固定数据库角色的成员。<br /><br /> 用于连接到发布服务器的帐户必须至少是发布数据库中的 **db_owner** 固定数据库角色的成员。<br /><br /> 如果选择 " `sync_type` *仅支持复制*" 选项、"*用备份初始化*" 或 "*从 lsn 初始化*" 选项，则日志读取器代理必须在执行后运行 `sp_addsubscription` ，以便将设置脚本写入分发数据库。 日志读取器代理必须在作为 **sysadmin** 固定服务器角色成员的帐户下运行。 当 `sync_type` 选项设置为 "*自动*" 时，不需要特殊的日志读取器代理操作。|  
|推送订阅的分发代理|与分发服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须：<br /><br /> -至少是分发数据库中**db_owner**固定数据库角色的成员。<br /><br /> -是 PAL 的成员。<br /><br /> -对快照共享拥有读取权限。<br /><br /> -如果订阅针对非 SQL Server 订阅服务器，则具备对订阅服务器的 OLE DB 访问接口的安装目录的访问权限。<br /><br /> -当复制 LOB 数据时，分发代理必须对复制 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 具有编写权限，其中 XX 表示实例 ID。<br /><br /> <br /><br /> 用于连接到订阅服务器的帐户必须至少是订阅数据库中的 **db_owner** 固定数据库角色的成员（或者如果订阅针对于非 SQL Server 订阅服务器，则必须具有同等权限）。<br /><br /> 注意：在 `-subscriptionstreams >= 2` 分发代理上使用时，还必须 `View Server State` 对订阅服务器授予权限，以便检测到死锁。|  
|请求订阅的分发代理|与订阅服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须至少是订阅数据库中的 **db_owner** 固定数据库角色的成员。 用于连接到分发服务器的帐户必须：<br /><br /> -是 PAL 的成员。<br /><br /> -对快照共享拥有读取权限。<br /><br /> -当复制 LOB 数据时，分发代理必须对复制 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 具有编写权限，其中 XX 表示实例 ID。<br /><br /> <br /><br /> 注意：在 `-subscriptionstreams >= 2` 分发代理上使用时，还必须 `View Server State` 对订阅服务器授予权限，以便检测到死锁。|  
|推送订阅的合并代理|与发布服务器和分发服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须：<br /><br /> -至少是分发数据库中**db_owner**固定数据库角色的成员。<br /><br /> -是 PAL 的成员。<br /><br /> -是与发布数据库中的某个用户关联的登录名。<br /><br /> -对快照共享拥有读取权限。<br /><br /> <br /><br /> 用于连接到订阅服务器的帐户必须至少是订阅数据库中的 **db_owner** 固定数据库角色的成员。|  
|请求订阅的合并代理|与订阅服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须至少是订阅数据库中的 **db_owner** 固定数据库角色的成员。 用于连接到发布服务器和分发服务器的帐户必须：<br /><br /> -是 PAL 的成员。<br /><br /> -是与发布数据库中的某个用户关联的登录名。<br /><br /> -是与分发数据库中的某个用户关联的登录名。 用户可以为 `Guest` 用户。<br /><br /> -对快照共享拥有读取权限。|  
|队列读取器代理|与分发服务器建立连接时，将使用运行代理的 Windows 帐户。 此帐户必须至少是分发数据库中的 **db_owner** 固定数据库角色的成员。<br /><br /> 用于连接到发布服务器的帐户必须至少是发布数据库中的 **db_owner** 固定数据库角色的成员。<br /><br /> 用于连接到订阅服务器的帐户必须至少是订阅数据库中的 **db_owner** 固定数据库角色的成员。|  
  
## <a name="agent-security-under-sql-server-agent"></a>SQL Server 代理下的代理安全性  
 使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 过程或 RMO 配置复制时，默认情况下将为每个代理创建 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理作业。 然后，代理将使用作业步骤的上下文运行，而不管它们是连续运行、根据计划运行还是按需运行。 可以在 **中的** Jobs [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]文件夹下查看这些作业。 下表列出了作业名称。  
  
|Agent|作业名称|  
|-----------|--------------|  
|快照代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|  
|合并发布分区的快照代理|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|  
|日志读取器代理|**\<Publisher>-\<PublicationDatabase>-\<integer>**|  
|请求订阅的合并代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|  
|推送订阅的合并代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|推送订阅的分发代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**<sup>1</sup>|  
|请求订阅的分发代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>**<sup>2</sup>|  
|非 SQL Server 订阅服务器的推送订阅的分发代理|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|队列读取器代理|**[\<Distributor>].\<integer>**|  
  
 <sup>1</sup>对于 Oracle 发布的推送订阅，作业名称为 * * \<Publisher> - \<Publisher**> 而不是 **\<Publisher>-\<PublicationDatabase>** 。  
  
 <sup>2</sup>对于 Oracle 发布的请求订阅，作业名称为 * * \<Publisher> - \<DistributionDatabase**> 而不是 **\<Publisher>-\<PublicationDatabase>** 。  
  
 配置复制时，指定运行代理应使用的帐户。 但是，所有作业步骤都使用“代理 **”的安全上下文运行；因此，复制会为指定的代理帐户在内部执行下列映射：  
  
-   首先使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql) 语句将帐户映射到凭据。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理的代理帐户使用凭据存储 Windows 用户帐户的相关信息。  
  
-   调用 [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) 存储过程，并使用凭据来创建代理。  
  
> [!NOTE]  
>  提供此信息有助于您了解使用适当的安全上下文运行代理时所涉及的内容。 您不需要与已创建的凭据或代理进行直接交互。  
  
## <a name="see-also"></a>另请参阅  
 [复制安全最佳做法](replication-security-best-practices.md)   
 [SQL Server 复制安全性](view-and-modify-replication-security-settings.md)   
 [保护快照文件夹的安全](secure-the-snapshot-folder.md)  
  
  
