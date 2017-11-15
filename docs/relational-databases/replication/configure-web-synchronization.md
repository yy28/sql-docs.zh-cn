---
title: "配置 Web 同步 | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
caps.latest.revision: "74"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 401c938c213b4e16bf8e63165f9875d84a1ea126
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="configure-web-synchronization"></a>配置 Web 同步
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 合并复制的 Web 同步选项支持使用 HTTPS 协议跨 Internet 复制数据。 若要使用 Web 同步，首先需要执行以下配置操作：  
  
1.  创建新的域帐户并映射 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
2.  配置运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet 信息服务 (IIS) 的计算机以同步订阅。  
  
3.  配置合并发布以允许使用 Web 同步。  
  
4.  配置一个或多个订阅以使用 Web 同步。  
  
> [!NOTE]  
>  如果您计划复制大量数据或者使用大型数据类型（如 **varchar(max)**），请阅读本主题中的“复制大量数据”一节。  
  
 若要成功设置 Web 同步，您必须决定如何配置安全性以满足您特定的要求和策略。 最好先作出以上决策并创建必要的帐户，然后再尝试配置 IIS、发布和订阅。  
  
 在之后的过程中，为简明起见，描述了一个使用本地帐户的简化安全配置。 这个简化的配置适用于 IIS 及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器和分发服务器同时运行在同一计算机上的安装情况，尽管您更可能对生产环境中的安装使用多服务器拓扑（也是建议做法）。 您可以在这些过程中用域帐户替代本地帐户。  
  
## <a name="creating-new-accounts-and-mapping-sql-server-logins"></a>创建新帐户并映射 SQL Server 登录名  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器 (replisapi.dll) 通过模拟为复制网站所关联的应用程序池指定的帐户来连接发布服务器。  
  
 用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器的帐户必须具有 [Merge Agent Security](../../relational-databases/replication/merge-agent-security.md)中的“连接发布服务器或分发服务器”一节所述的权限。 总之，该帐户必须：  
  
-   是发布访问列表 (PAL) 的成员。  
  
-   映射到与发布数据库中的某个用户关联的登录名。  
  
-   映射到与分发数据库中的某个用户关联的登录名。  
  
-   对快照共享具有读取权限。  
  
 如果您是首次使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制，您还需要为复制代理创建帐户和登录名。 有关详细信息，请参阅本主题中的“配置发布”和“配置订阅”这两节。  
  
 在配置 Web 同步前，建议您先阅读本主题中的“Web 同步的最佳安全配置”一节。 有关 Web 同步安全性的详细信息，请参阅 [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)。  
  
## <a name="configuring-the-computer-that-is-running-iis"></a>配置正在运行 IIS 的计算机  
 Web 同步要求安装并配置 IIS。 在配置发布以使用 Web 同步之前，您需要了解复制网站的 URL。  
  
 从版本 5.0 开始，IIS 中支持 Web 同步。 IIS 版本 7.0 不支持配置 Web 同步向导。 从 SQL Server 2012 开始，要使用 IIS 服务器上的 Web 同步组件，我们建议用户随复制安装 SQL Server。 这可以是免费的 SQL Server Express 版本。  
  
 需要使用 SSL 进行 Web 同步。 您将需要由证书颁发机构颁发的安全证书。 仅出于测试目的，可以使用自行颁发的安全证书。  
   
  
 **配置 IIS 以实现 Web 同步**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][配置 IIS 以实现 Web 同步](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[配置 IIS 7 以实现 Web 同步](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## <a name="creating-a-web-garden"></a>创建 Web 园  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器支持每个线程处理两个并发同步操作。 超出此限制可能导致复制侦听器停止响应。 为 replisapi.dll 分配的线程数由应用程序池的 Maximum Worker Processes 属性来确定。 默认情况下，此属性设置为 1。  
  
 您可以通过增大 Maximum Worker Process 属性值来支持每个 CPU 处理更多的并发同步操作。 通过增大每个 CPU 的工作进程数进行扩展的方式被称为创建“Web 园”。  
  
 创建 Web 园将允许同时有两个以上的订阅服务器进行同步。 但这也会增加 replisapi.dll 对 CPU 的占用，从而给服务器总体性能带来负面影响。 所以在选择 Maximum Worker Processes 的值时务须权衡考虑以上两个方面。  
  
#### <a name="to-increase-maximum-worker-processes-in-iis-7"></a>在 IIS 7 中增加最大工作进程数  
  
1.  在 **“Internet 信息服务(IIS)管理器”**中，展开本地服务器节点，然后单击 **“应用程序池”** 节点。  
  
2.  选择与 Web 同步站点关联的应用程序池，然后单击 **“操作”** 窗格上的 **“高级设置”** 。  
  
3.  在“高级设置”对话框的 **“处理模型”** 标题下，单击标为 **“最大工作线程数”**的行。 更改属性值，然后单击 **“确定”**。  
  
## <a name="configuring-the-publication"></a>配置发布  
 若要使用 Web 同步，需要创建一个发布（就像为标准合并拓扑创建发布一样）。 有关详细信息，请参阅[发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
 创建发布后，启用允许通过以下方法之一（ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或复制管理对象 (RMO)）进行 Web 同步的选项。 若要启用 Web 同步，需要为订阅服务器连接提供 Web 服务器地址。  
  
 如果您是首次使用发布服务器，还必须配置分发服务器和快照共享。 每台订阅服务器中的合并代理都必须对快照共享具有读取权限。 有关详细信息，请参阅[配置分发](../../relational-databases/replication/configure-distribution.md)和[保护快照文件夹的安全](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
 **gen** 是 websync xml 文件中的一个保留字。 不要尝试发布包含名为 **gen**的列的表。  
  
## <a name="configuring-the-subscription"></a>配置订阅  
 启用发布并配置 IIS 后，创建请求订阅并指定该请求订阅应通过使用 IIS 进行同步。 （仅请求订阅支持 Web 同步。）  
  
## <a name="upgrading-from-an-earlier-version-of-sql-server"></a>升级 SQL Server 的早期版本  
 如果您现在配置有 Web 同步拓扑，并且要升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则必须将 Replisapi.dll 的最新版本复制到 Web 同步所用的虚拟目录。 默认情况下，Replisapi.dll 的最新版本位于 C:\Program Files\Microsoft SQL Server\\<nnn\>\COM 中。  
  
## <a name="replicating-large-volumes-of-data"></a>复制大量数据  
 为避免订阅服务器计算机出现潜在的内存问题，Web 同步对用于传输更改的 XML 文件使用默认最大大小 100 MB。 可以通过设置以下注册表项来引发限制：  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 此注册表项可接受值的范围是 100 MB 到 4GB。 值以 KB 指定。 将此参数设置为高值并不保证您能够同步该数量的数据。 有效限制值受订阅服务器计算机上的可用连续内存量约束。 如果您的值必须大于 100 MB，建议您递增该值，并且使用订阅服务器上的典型工作负荷来测试内存占用。  
  
 XML 文件的最大大小为 4 GB，但复制会成批地同步该文件的更改。 数据和元数据的最大批大小是 25 MB。 必须确保每批的数据不超过大约 20 MB，20 MB 足以容纳元数据和任何其他开销。 此限制具有以下含义：  
  
-   不能复制任何会导致数据和元数据超过 25 MB 的列。 如果要复制的行包含大型数据类型（如 **varchar(max)**），这可能会引发问题。  
  
-   如果要复制大量数据，则可能必须调整合并代理的批大小。  
  
 合并复制的批大小是用“ 代”度量的，代是指每个项目的变更集。 每个批次中代的数量是使用合并代理的 **DownloadGenerationsPerBatch** 和 **UploadGenerationsPerBatch** 参数指定的。 有关详细信息，请参阅 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
 对于大量数据，请为每个批次参数指定一个较小的数字。 我们建议您从值 10 开始，然后基于应用程序需要和性能进行调整。 通常，这些参数在代理配置文件中指定。 有关配置文件的详细信息，请参阅 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
## <a name="security-best-practices-for-web-synchronization"></a>Web 同步的最佳安全配置  
 在 Web 同步中，有很多与安全相关的设置可供选择。 建议使用以下方法：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分发服务器和发布服务器可位于同一台计算机上（这是合并复制的典型安装）。 但是，IIS 应该安装在单独的计算机上。  
  
-   使用安全套接字层 (SSL) 加密订阅服务器和运行 IIS 的计算机之间的连接。 这对 Web 同步是必需的。  
  
-   对从订阅服务器到 IIS 的连接使用基本身份验证。 使用基本身份验证，IIS 服务器无需委托，就可以代表订阅服务器与发布服务器/分发服务器建立连接。 如果使用集成身份验证，则必须使用委托。  
  
    > [!NOTE]  
    >  基本身份验证是将凭据传递给 IIS 时所采用的方法。 基本身份验证不会阻止为与 IIS 建立的连接指定 Windows 域帐户。  
  
-   指定快照代理应以 Windows 域帐户运行，并指定代理应以该帐户建立连接。 （这是默认配置。）指定每个合并代理都应以使用订阅服务器计算机的用户的域帐户运行，并指定代理应以该帐户建立连接。  
  
     有关代理所需权限的详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
-   指定与合并代理在执行任务（在新建订阅向导的 **“Web 服务器信息”** 页中指定帐户和密码，或指定 **@internet_url** 和 **@internet_login** 和 [@internet_login](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 此帐户必须具有对快照共享的读取权限。  
  
-   每个发布都应对 IIS 使用一个单独的虚拟目录。  
  
-   运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器 (Replisapi.dll) 的帐户也是要在同步期间连接到发布服务器和分发服务器的帐户。 此帐户必须映射到发布服务器和分发服务器上的 SQL 登录帐户。 有关详细信息，请参阅[配置 IIS 以实现 Web 同步](../../relational-databases/replication/configure-iis-for-web-synchronization.md)中的“设置 SQL Server 复制侦听器的权限”一节。  
  
-   可以使用 FTP 将快照从发布服务器传递到运行 IIS 的计算机。 快照始终使用 HTTPS 从运行 IIS 的计算机传递到订阅服务器。 有关详细信息，请参阅[通过 FTP 传输快照](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
-   如果复制拓扑中的服务器位于防火墙之后，则需要在防火墙中打开端口以便启用 Web 同步。  
  
    -   订阅服务器计算机使用 SSL 通过 HTTPS（通常配置为使用端口 443）连接到运行 IIS 的计算机。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器还可以通过 HTTP（通常配置为使用端口 80）建立连接。  
  
    -   运行 IIS 的计算机通常通过端口 1433 连接到发布服务器或分发服务器（默认实例）。 当发布服务器或分发服务器是某台服务器上的命名实例，且该服务器具有另一个默认实例时，则通常通过端口 1500 连接到命名实例。  
  
    -   如果运行 IIS 的计算机与分发服务器被防火墙隔离开来，且快照传送使用的是 FTP 共享，则必须打开用于 FTP 的端口。 有关详细信息，请参阅[通过 FTP 传输快照](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
> [!IMPORTANT]  
>  打开防火墙的端口可能会使服务器受到恶意攻击。 请确保在打开端口之前了解防火墙系统。 有关详细信息，请参阅 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [合并复制的 Web 同步](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
