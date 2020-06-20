---
title: 企业范围的自动化管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8df3e34c2c70c81f9710ade0d6855446b930fb50
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011802"
---
# <a name="automated-administration-across-an-enterprise"></a>企业范围的自动化管理
  跨多个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的自动化管理称为“多服务器管理”**。 使用多服务器管理可以执行下列操作：  
  
-   管理两台或多台服务器。  
  
-   在企业服务器之间安排数据仓库的信息流。  
  
> [!NOTE]  
>  作为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不断降低总拥有成本的一项工作的一部分， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了两项功能：管理称为基于策略的管理的服务器的方法，以及使用配置服务器和服务器组的多服务器查询。 这些功能可以与本主题中介绍的某些功能一起使用，也可能会替代这些功能。 有关详细信息，请参阅使用[基于策略的管理来管理服务器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)和[使用中央管理服务器管理多台服务器](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)。  
  
 若要利用多服务器管理，您必须至少有一台主服务器且至少有一台目标服务器。 主服务器将作业分发到目标服务器并从它那里接收事件。 主服务器还存储在目标服务器上运行的作业的作业定义的中央副本。 目标服务器定期连接到主服务器来更新它们的作业计划。 如果主服务器上存在新作业，目标服务器将下载该作业。 目标服务器在完成作业后，会重新连接到主服务器并报告作业状态。  
  
 以下图例显示了主服务器与目标服务器之间的关系。  
  
 ![多服务器管理配置](../../database-engine/media/multisvr.gif "多服务器管理配置")  
  
 如果管理大公司内的部门服务器，则可以定义以下内容：  
  
-   一个包含作业步骤的备份作业。  
  
-   备份失败时通知的操作员。  
  
-   备份作业的执行计划。  
  
 将该备份作业一次性写入主服务器，然后将部门服务器登记为目标服务器。 从它们登记时刻起，所有部门服务器将运行相同的备份作业，而您只需定义一次作业。  
  
> [!NOTE]  
>  多服务器管理功能用于 sysadmin 角色成员。 然而，目标服务器上的 sysadmin 角色成员无法编辑目标服务器上由主服务器执行的操作。 这项安全措施可防止意外删除作业步骤，并可防止目标服务器上的操作中断。  
  
## <a name="in-this-section"></a>本节内容  
 [创建多服务器环境](create-a-multiserver-environment.md)  
 包含有关如何创建和管理主服务器和目标服务器的信息。  
  
 [为多服务器环境选择正确的 SQL Server 代理服务帐户](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
 包含有关使用非管理 Windows 帐户或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理服务的本地系统帐户如何影响多服务器环境的信息。  
  
 [在目标服务器上设置加密选项](set-encryption-options-on-target-servers.md)  
 包含有关在目标服务器上设置 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理注册表子项 MsxEncryptChannelOptions 的信息。  
  
 [管理整个企业内的作业](manage-jobs-across-an-enterprise.md)  
 包含有关检查作业状态、更改作业的目标服务器、同步目标服务器时钟以及轮询主服务器以获取当前作业状态的信息。  
  
 [排除使用代理的多服务器作业的故障](troubleshoot-multiserver-jobs-that-use-proxies.md)  
 包含有关排除使用失败代理的多服务器作业故障的信息。  
  
 [轮询服务器](poll-servers.md)  
 包含有关如何隐式和显式使目标服务器轮询主服务器以同步作业信息的信息。  
  
 [管理事件](manage-events.md)  
 包含有关将事件从目标服务器转发到主服务器的信息。  
  
 [在企业中优化自动化管理](tune-automated-administration-across-an-enterprise.md)  
 包含有关多服务器环境中的自动化管理如何利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]自我优化功能的信息。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 数据库引擎的向后兼容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [注册服务器](../register-servers/register-servers.md)   
 [sp_add_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql)   
 [sp_delete_targetserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql)   
 [sp_delete_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql)   
 [sp_help_downloadlist &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql)   
 [sp_help_jobserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql)   
 [sp_help_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)   
 [sp_resync_targetserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)   
 [sp_update_targetservergroup &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql)   
 [dbo.sysjobservers &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobservers-transact-sql)   
 [Transact-sql&#41;sys.sys登录名 &#40;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)   
 [dbo.systargetservers &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-systargetservers-transact-sql)  
  
  
