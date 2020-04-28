---
title: 配置发布和分发 | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- publishing [SQL Server replication], configuring
ms.assetid: 3cfc8966-833e-42fa-80cb-09175d1feed7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 905b1ceed2df8afc854ad38ee07d2b21596530f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882256"
---
# <a name="configure-publishing-and-distribution"></a>配置发布和分发
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中配置发布和分发。  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[安全复制部署](security/view-and-modify-replication-security-settings.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可以使用新建发布向导或配置分发向导配置分发。 配置分发服务器后，查看并修改“分发服务器属性 - **分发服务器>”\<** 对话框中的属性。 如果要配置分发服务器以使 **db_owner** 固定数据库角色的成员可以创建发布，或者要配置一个非发布服务器的远程分发服务器，请使用配置分发向导。  
  
#### <a name="to-configure-distribution"></a>配置分发  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，连接到将要作为分发服务器的服务器（许多情况下，发布服务器和分发服务器是同一服务器），然后展开该服务器节点。  
  
2.  右键单击 **“复制”** 文件夹，然后单击 **“配置分发”** 。  
  
3.  随着配置分发向导执行下列操作：  
  
    -   选择分发服务器。 若要使用本地分发服务器，请选择 **"\<ServerName>" 将充当自己的分发服务器;SQL Server 将创建分发数据库和日志**。 若要使用远程分发服务器，请选择 **“使用以下服务器作为分发服务器”** ，再选择一个服务器。 该服务器必须已配置为分发服务器，并且启用发布服务器使用此分发服务器。 有关详细信息，请参阅[在分发服务器上启用远程发布服务器 (SQL Server Management Studio)](enable-a-remote-publisher-at-a-distributor-sql-server-management-studio.md)。  
  
         如果选择远程分发服务器，则必须在 **“管理密码”** 页上输入从发布服务器连接到分发服务器的密码。 此密码必须与在远程分发服务器上启用发布服务器时所指定的密码相匹配。  
  
    -   指定根快照文件夹（适用于本地分发服务器）。 快照文件夹只是指定共享的目录。向此文件夹中执行读写操作的代理必须对其具有足够的访问权限。 每个使用此分发服务器的发布服务器都在根文件夹下创建一个文件夹，而每个发布则在发布服务器文件夹下创建用于存储快照文件的文件夹。 有关正确保护文件夹的详细信息，请参阅[保护快照文件夹的安全](security/secure-the-snapshot-folder.md)。  
  
    -   指定分发数据库（适用于本地分发服务器）。 分发数据库存储事务性复制的所有复制和事务类型的元数据和历史记录数据。  
  
    -   还可以让其他发布服务器使用该分发服务器（可选）。 如果其他发布服务器能够使用分发服务器，则必须在 **“分发服务器密码”** 页上输入从这些发布服务器连接到分发服务器的密码。  
  
    -   还可以为配置设置编写脚本（可选）。 有关详细信息，请参阅 [Scripting Replication](scripting-replication.md)。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式配置复制发布和分发。  
  
#### <a name="to-configure-publishing-using-a-local-distributor"></a>使用本地分发服务器配置发布  
  
1.  执行 [sp_get_distributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql) 以确定服务器是否已配置为分发服务器。  
  
    -   如果结果集中 **installed** 的值为 **0**，请在分发服务器上对 master 数据库执行 [sp_adddistributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)。  
  
    -   如果结果集中 **distribution db installed** 的值为 **0**，请在分发服务器上对 master 数据库执行 [sp_adddistributiondb (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)。 指定** \@数据库**的分发数据库的名称。 还可以指定** \@max_distretention**的最大事务保持期和** \@history_retention**的历史记录保持期。 如果要创建一个新的数据库，请指定所需的数据库属性参数。  
  
2.  在同时作为发布服务器的分发服务器上，执行[sp_adddistpublisher &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)，并指定将用作** \@working_directory**默认快照文件夹的 UNC 共享。  
  
3.  在发布服务器上执行 [sp_replicationdboption (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)。 为 "数据库类型" 指定要** \@发布的数据库，为** ** \@optname**指定复制的类型，并`true`为 " ** \@值**" 指定值。  
  
#### <a name="to-configure-publishing-using-a-remote-distributor"></a>使用远程分发服务器配置发布  
  
1.  执行 [sp_get_distributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql) 以确定服务器是否已配置为分发服务器。  
  
    -   如果结果集中 **installed** 的值为 **0**，请在分发服务器上对 master 数据库执行 [sp_adddistributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)。 指定** \@密码**的强密码。 发布服务器在连接到分发服务器时将使用 **distributor_admin** 帐户的此密码。  
  
    -   如果结果集中 **distribution db installed** 的值为 **0**，请在分发服务器上对 master 数据库执行 [sp_adddistributiondb (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)。 指定** \@数据库**的分发数据库的名称。 还可以指定** \@max_distretention**的最大事务保持期和** \@history_retention**的历史记录保持期。 如果要创建一个新的数据库，请指定所需的数据库属性参数。  
  
2.  在分发服务器上，执行[sp_adddistpublisher &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)，并指定将用作** \@working_directory**默认快照文件夹的 UNC 共享。 如果分发服务器在连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到发布服务器时将使用身份验证，则还必须将** \@security_mode**的值指定为**0** ，并[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将登录信息指定为** \@登录**名和** \@密码**。  
  
3.  在发布服务器上，对 master 数据库执行 [sp_adddistributor (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)。 为** \@密码**指定在步骤1中使用的强密码。 发布服务器在连接到分发服务器时将使用此密码。  
  
4.  在发布服务器上执行 [sp_replicationdboption (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)。 为 "数据库类型" 指定要** \@发布的数据库，为** ** \@optname**指定复制的类型，并将 " ** \@值**" 的值指定为 "true"。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例说明了如何以编程方式配置发布和分发。 在本示例中，使用脚本变量提供要配置为发布服务器和本地分发服务器的服务器的名称。 可以使用复制存储过程以编程方式配置复制发布和分发。  
  
 [!code-sql[HowTo#AddDistPub](../../snippets/tsql/SQL15/replication/howto/tsql/adddistpub.sql#adddistpub)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
  
#### <a name="to-configure-publishing-and-distribution-on-a-single-server"></a>在单个服务器上配置发布和分发  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与服务器的连接。  
  
2.  创建的 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类的实例。 传递步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
3.  创建的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 类的实例。  
  
4.  将 <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> 属性设置为数据库名称，并将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
5.  通过调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 方法安装分布服务器。 传递步骤 3 中的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 对象。  
  
6.  创建的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 类的实例。  
  
7.  设置 <xref:Microsoft.SqlServer.Replication.DistributionPublisher>的以下属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - 发布服务器的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> - 在步骤 5 中创建的数据库的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> - 用于访问快照文件的共享目录。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> - 连接到发布服务器时使用的安全模式。 建议使用<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 。  
  
8.  调用 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> 方法。  
  
#### <a name="to-configure-publishing-and-distribution-using-a-remote-distributor"></a>使用远程分发服务器配置发布和分发  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与远程分发服务器的连接。  
  
2.  创建的 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类的实例。 传递步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
3.  创建的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 类的实例。  
  
4.  将 <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> 属性设置为数据库名称，并将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
5.  通过调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 方法安装分布服务器。 指定安全密码（在连接到远程分发服务器时由发布服务器使用）和步骤 3 中的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 对象。 有关详细信息，请参阅[保护分发服务器的安全](security/secure-the-distributor.md)。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework 提供的[加密服务](https://go.microsoft.com/fwlink/?LinkId=34733)。  
  
6.  创建的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 类的实例。  
  
7.  设置 <xref:Microsoft.SqlServer.Replication.DistributionPublisher>的以下属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - 本地发布服务器的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> - 在步骤 5 中创建的数据库的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> - 用于访问快照文件的共享目录。  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> - 连接到发布服务器时使用的安全模式。 建议使用<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 。  
  
8.  调用 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> 方法。  
  
9. 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与本地发布服务器的连接。  
  
10. 创建的 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类的实例。 传递步骤 9 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
11. 调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 方法。 传递远程分发服务器的名称和在步骤 5 中指定的远程分发服务器的密码。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 Windows .NET Framework 提供的 [Cryptographic Services](https://go.microsoft.com/fwlink/?LinkId=34733) （加密服务）。  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a>示例（RMO）  
 可以通过使用复制管理对象 (RMO) 以编程方式配置复制发布和分发。  
  
 [!code-csharp[HowTo#rmo_AddDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_adddistpub)]  
  
 [!code-vb[HowTo#rmo_vb_AddDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_adddistpub)]  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)   
 [复制系统存储过程概念](concepts/replication-system-stored-procedures-concepts.md)   
 [配置分发](configure-distribution.md)   
 [复制管理对象概念](concepts/replication-management-objects-concepts.md)   
 [为 AlwaysOn 可用性组 &#40;SQL Server 配置复制&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) 
  
  
