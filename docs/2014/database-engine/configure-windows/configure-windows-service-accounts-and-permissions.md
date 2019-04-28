---
title: 配置 Windows 服务帐户和权限 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- startup service states [SQL Server]
- Setup [SQL Server], user accounts
- Windows permissions [SQL Server]
- modifying user accounts
- default accounts
- domains [SQL Server], user accounts
- startup accounts [SQL Server]
- system accounts [SQL Server]
- services [SQL Server], permissions
- ACL (access control list)
- local system accounts [SQL Server]
- instance-aware services [SQL Server]
- permissions [SQL Server], services
- SQL Server Agent service, user accounts
- Windows NT permissions [SQL Server]
- user accounts [SQL Server]
- identifying instance-unaware services [SQL Server]
- installing SQL Server, user accounts
- disabled startup state [SQL Server]
- user accounts [SQL Server], users
- Local Service account [SQL Server]
- SQL Server Installation Wizard
- instance-unaware services [SQL Server]
- services [SQL Server], configuring at installation
- Windows accounts [SQL Server]
- SQL Server services, user accounts
- user accounts [SQL Server], services
- MSSQLServer
- identifying instance-aware services [SQL Server]
- services [SQL Server], accounts
- access control lists
- optional accounts [SQL Server]
- service accounts [SQL Server]
- accounts [SQL Server], services
- built-in system accounts [SQL Server]
- automatic startup state
- domains [SQL Server]
- manual startup state [SQL Server]
- accounts [SQL Server], user
ms.assetid: 309b9dac-0b3a-4617-85ef-c4519ce9d014
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4ed6f335e3a791d4af8b780527d963115439a7f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787807"
---
# <a name="configure-windows-service-accounts-and-permissions"></a>配置 Windows 服务帐户和权限
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每个服务表示一个进程或一组进程，用于通过 Windows 管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作的身份验证。 本主题介绍此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中服务的默认配置，以及可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中以及安装之后设置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的配置选项。  
  
##  <a name="Top"></a> 内容  
 本主题分为以下几个部分：  
  
-   [安装的 SQL Server 服务](#Service_Details)  
  
-   [服务属性和配置](#Serv_Prop)  
  
    -   [默认服务帐户](#Default_Accts)  
  
        -   [更改帐户属性](#Changing_Accounts)  
  
    -   [适用于 Windows 7 和 Windows Server 2008 R2 的新帐户类型](#New_Accounts)  
  
    -   [自动启动](#Auto_Start)  
  
    -   [无人参与安装过程中配置服务](#Configure_services)  
  
    -   [防火墙端口](#Firewall)  
  
-   [服务权限](#Serv_Perm)  
  
    -   [服务配置和访问控制](#Serv_SID)  
  
    -   [Windows 特权和权限](#Windows)  
  
    -   [文件系统权限授予 SQL Server per-service Sid 或本地 Windows 组](#Reviewing_ACLs)  
  
    -   [文件系统权限授予其他 Windows 用户帐户或组](#File_System_Other)  
  
    -   [与非寻常磁盘位置相关的文件系统权限](#Unusual_Locations)  
  
    -   [查看其他注意事项](#Review_additional_considerations)  
  
    -   [注册表权限](#Registry)  
  
    -   [WMI](#WMI)  
  
    -   [命名管道](#Pipes)  
  
-   [预配](#Provisioning)  
  
    -   [数据库引擎预配](#DE_Prov)  
  
        -   [Windows 主体](#Win_Principals)  
  
        -   [sa 帐户](#sa)  
  
        -   [SQL Server Per-service SID 登录名和特权](#Logins)  
  
        -   [SQL Server 代理登录名和特权](#Agent)  
  
        -   [HADRON 和 SQL 故障转移群集实例和特权](#Hadron)  
  
        -   [SQL 编写器和特权](#Writer)  
  
        -   [SQL WMI 和特权](#SQLWMI)  
  
    -   [SSAS 预配](#SSAS)  
  
    -   [SSRS 预配](#SSRS)  
  
-   [从早期版本升级](#Upgrade)  
  
-   [Appendix](#Appendix)  
  
    -   [服务帐户的描述](#Serv_Accts)  
  
    -   [辨别识别实例的服务和不识别实例的服务](#Identify_instance_aware_and_unaware)  
  
    -   [本地化的服务名称](#Localized_service_names)  
  
##  <a name="Service_Details"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的服务  
 根据您决定安装的组件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将安装以下服务：  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Services** - 用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的服务。 可执行文件为 \<MSSQLPATH>\MSSQL\Binn\sqlservr.exe。  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理** - 执行作业、监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、激发警报以及允许自动执行某些管理任务。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]的实例上存在，但处于禁用状态。 可执行文件为 \<MSSQLPATH>\MSSQL\Binn\sqlagent.exe。  
  
-   **[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]**  - 为商业智能应用程序提供联机分析处理 (OLAP) 和数据挖掘功能。 可执行文件为 \<MSSQLPATH>\OLAP\Bin\msmdsrv.exe。  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  - 管理、执行、创建、计划和传递报表。 可执行文件为 \<MSSQLPATH>\Reporting Services\ReportServer\Bin\ReportingServicesService.exe。  
  
-   **[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]**  - 为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的存储和执行提供管理支持。 可执行文件的路径是\<MSSQLPATH > \120\DTS\Binn\MsDtsSrvr.exe  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser** - 向客户端计算机提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接信息的名称解析服务。 可执行文件的路径为 c:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe  
  
-   **全文搜索** - 对结构化和半结构化数据的内容和属性快速创建全文索引，从而为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供文档筛选和断字功能。  
  
-   **SQL 编写器** - 允许备份和还原应用程序在卷影复制服务 (VSS) 框架中运行。  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分布式重播控制器** - 跨多个分布式重播客户端计算机提供跟踪重播业务流程。  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 客户端** - 与 Distributed Replay 控制器一起来模拟针对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例的并发工作负荷的一台或多台 Distributed Replay 客户端计算机。  
  
##  <a name="Serv_Prop"></a> 服务属性和配置  
 用于启动和运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的启动帐户可以是 [域用户帐户](#Domain_User)、 [本地用户帐户](#Local_User)、 [托管服务帐户](#MSA)、 [虚拟帐户](#VA_Desc)或 [内置系统帐户](#Local_Service)。 若要启动和运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每项服务，这些服务都必须有一个在安装过程中配置的启动帐户。  
  
 此部分介绍可配置为启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序使用的默认值、Per-service SID 的概念、启动选项以及配置防火墙。  
  
-   [默认服务帐户](#Default_Accts)  
  
-   [自动启动](#Auto_Start)  
  
-   [配置服务启动类型](#Configure_services)  
  
-   [防火墙端口](#Firewall)  
  
###  <a name="Default_Accts"></a> 默认服务帐户  
 下表列出了安装程序在安装所有组件时使用的默认服务帐户。 列出的默认帐户是建议使用的帐户，但特殊注明的除外。  
  
 **独立服务器或域控制器**  
  
|组件|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|Windows 7 和 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 及更高版本|  
|---------------|------------------------------------|----------------------------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 控制器|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 客户端|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc) <sup>*</sup>|  
|FD 启动器（全文搜索）|[LOCAL SERVICE](#Local_Service)|[虚拟帐户](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[LOCAL SERVICE](#Local_Service)|[LOCAL SERVICE](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 编写器|[LOCAL SYSTEM](#Local_System)|[LOCAL SYSTEM](#Local_System)|  
  
 <sup>*</sup> 当外部的资源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所需计算机，[!INCLUDE[msCoName](../../includes/msconame-md.md)]建议使用托管服务帐户 (MSA)，使用所需的最低权限配置。  
  
 **SQL Server 故障转移群集实例**  
  
|组件|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2|  
|---------------|------------------------------------|---------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|无。 提供 [域用户](#Domain_User) 帐户。|提供 [域用户](#Domain_User) 帐户。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理|无。 提供 [域用户](#Domain_User) 帐户。|提供 [域用户](#Domain_User) 帐户。|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|无。 提供 [域用户](#Domain_User) 帐户。|提供 [域用户](#Domain_User) 帐户。|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc)|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[NETWORK SERVICE](#Network_Service)|[虚拟帐户](#VA_Desc)|  
|FD 启动器（全文搜索）|[LOCAL SERVICE](#Local_Service)|[虚拟帐户](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[LOCAL SERVICE](#Local_Service)|[LOCAL SERVICE](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 编写器|[LOCAL SYSTEM](#Local_System)|[LOCAL SYSTEM](#Local_System)|  
  
####  <a name="Changing_Accounts"></a> 更改帐户属性  
  
> [!IMPORTANT]
>  -   始终使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具（例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器）来更改 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务使用的帐户，或更改帐户的密码。 除了更改帐户名称以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器还可以执行其他配置，例如，更新保护 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的服务主密钥的 Windows 本地安全存储区。 其他工具（例如 Windows 服务控制管理器）可以更改帐户名称，但不更改所有必需的设置。  
> -   对于您在 SharePoint 场中部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，始终使用 SharePoint 管理中心为 [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] 应用程序和 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]更改服务器帐户。 使用管理中心时，关联的设置和权限将更新为使用新的帐户信息。  
> -   若要更改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 选项，请使用 Reporting Services 配置工具。  
  
###  <a name="New_Accounts"></a> 适用于 Windows 7 和 Windows Server 2008 R2 的新帐户类型  
 Windows 7 和 Windows Server 2008 R2 有两种新型的服务帐户，即托管服务帐户 (MSA) 和虚拟帐户。 托管服务帐户和虚拟帐户设计用于向关键应用程序（例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）提供其自己帐户的隔离，同时使管理员无需手动管理这些帐户的服务主体名称 (SPN) 和凭据。 这就使得管理服务帐户用户、密码和 SPN 的过程变得简单得多。  
  
-   <a name="MSA"></a> **Managed Service Accounts**  
  
     托管服务帐户 (MSA) 是一种由域控制器创建和管理的域帐户。 它分配给单个成员计算机以用于运行服务。 域控制器将自动管理密码。 您不能使用 MSA 登录到计算机，但计算机可以使用 MSA 来启动 Windows 服务。 MSA 可以向 Active Directory 注册服务主体名称 (SPN)。 MSA 的名称中有一个 **$** 后缀，例如 **DOMAIN\ACCOUNTNAME$**。 在指定 MSA 时，请将密码留空。 因为将 MSA 分配给单个计算机，它不能用于 Windows 群集的不同节点。  
  
    > [!NOTE]  
    >  域管理员必须先在 Active Directory 中创建 MSA，然后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序才能将其用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
    
-  <a name="GMSA"></a>**组托管服务帐户**  
  
     组托管服务帐户是针对多个服务器的 MSA。 Windows 为在一组服务器上运行的服务管理服务帐户。 Active Directory 自动更新组托管服务帐户密码，而不重启服务。 你可以配置 SQL Server 服务以使用组托管服务帐户主体。 从 SQL Server 2014 开始，SQL Server 针对独立实例、故障转移群集实例和可用性组，在 Windows Server 2012 R2 和更高版本上支持组托管服务帐户。  
  
    若要使用 SQL Server 2014 或更高版本的组托管服务帐户，操作系统必须是 Windows Server 2012 R2 或更高版本。 装有 Windows Server 2012 R2 的服务器需要应用 [KB 2998082](https://support.microsoft.com/kb/2998082) ，以便服务可以在密码更改后立即登录而不中断。  
  
    有关详细信息，请参阅 [组托管服务帐户](https://technet.microsoft.com/library/hh831782.aspx)  
      
    > [!NOTE]  
    >  域管理员必须先在 Active Directory 中创建组托管服务帐户，然后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序才能将其用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 
  
-   <a name="VA_Desc"></a> **虚拟帐户**  
  
     虚拟帐户（从 Windows Server 2008 R2 和 Windows 7 开始）是“托管的本地帐户”  ，此类帐户提供以下功能，可简化服务管理。 虚拟帐户是自动管理的，并且虚拟帐户可以访问域环境中的网络。 如果在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 期间对服务帐户使用默认值，则将使用将实例名称用作服务名称的虚拟帐户，格式为 NT SERVICE\\\<SERVICENAME>。 以虚拟帐户身份运行的服务通过使用计算机帐户的凭据（格式为 _<domain_name>_**\\**_<computer_name>_**$**）访问网络资源。  当指定一个虚拟帐户以启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，应将密码留空。 如果虚拟帐户无法注册服务主体名称 (SPN)，则手动注册该 SPN。 有关手动注册 SPN 的详细信息，请参阅 [手动注册 SPN](register-a-service-principal-name-for-kerberos-connections.md#Manual)。  
  
    > [!NOTE]  
    >  虚拟帐户不能用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例，因为虚拟帐户在群集的每个节点不会有相同 SID。  
  
     下表列出了虚拟帐户名称的示例。  
  
    |服务|虚拟帐户名称|  
    |-------------|--------------------------|  
    |[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务的默认实例|**NT SERVICE\MSSQLSERVER**|  
    |名为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 **的**服务的命名实例|**NT SERVICE\MSSQL$PAYROLL**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务，位于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|**NT SERVICE\SQLSERVERAGENT**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务，位于名为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PAYROLL **的**|**NT SERVICE\SQLAGENT$PAYROLL**|  
  
 有关托管服务帐户和虚拟帐户的详细信息，请参阅 **服务帐户分步指南** 的 [托管服务和虚拟帐户概念](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx) 部分以及 [托管服务帐户常见问题解答 (FAQ)](https://technet.microsoft.com/library/ff641729\(WS.10\).aspx)。  
  
 **安全说明：** 只要可能，[!INCLUDE[ssNoteLowRights](../../includes/ssnotelowrights-md.md)] 就会使用 [MSA](#MSA) 或[虚拟帐户](#VA_Desc)。 当无法使用 MSA 和虚拟帐户时，将使用特定的低特权用户帐户或域帐户，而不将共享帐户用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 对不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务使用单独的帐户。 不要向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户或服务组授予其他权限。 在支持服务 SID 的情况下，将通过组成员身份或直接将权限授予服务 SID。  
  
###  <a name="Auto_Start"></a> 自动启动  
 除了具有用户帐户外，每项服务还有用户可控制的三种可能的启动状态：  
  
-   **已禁用** 服务已安装但当前未运行。  
  
-   **手动** 服务已安装，但仅当另一个服务或应用程序需要该服务的功能时才启动。  
  
-   **自动** 服务由操作系统自动启动。  
  
 在安装过程中，启动状态处于选中状态。 当安装命名实例时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务应设置为自动启动。  
  
###  <a name="Configure_services"></a> 在无人参与的安装过程中配置服务  
 下表显示了可以在安装过程中配置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 对于无人参与的安装，可以在配置文件中或在命令提示符下使用开关。  
  
|SQL Server 服务名称|无人参与安装的开关<sup>1</sup>|  
|-----------------------------|-------------------------------------------------------|  
|MSSQLSERVER|SQLSVCACCOUNT、SQLSVCPASSWORD、SQLSVCSTARTUPTYPE|  
|SQLServerAgent<sup>2</sup>|AGTSVCACCOUNT、AGTSVCPASSWORD、AGTSVCSTARTUPTYPE|  
|MSSQLServerOLAPService|ASSVCACCOUNT、ASSVCPASSWORD、ASSVCSTARTUPTYPE|  
|ReportServer|RSSVCACCOUNT、RSSVCPASSWORD、RSSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|ISSVCACCOUNT、ISSVCPASSWORD、ISSVCSTARTUPTYPE|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 控制器|DRU_CTLR、CTLRSVCACCOUNT、CTLRSVCPASSWORD、CTLRSTARTUPTYPE、CTLRUSERS|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 客户端|DRU_CLT、CLTSVCACCOUNT、CLTSVCPASSWORD、CLTSTARTUPTYPE、CLTCTLRNAME、CLTWORKINGDIR、CLTRESULTDIR|  
  
 <sup>1</sup>有关详细信息和无人参与安装的示例语法，请参阅[从命令提示符安装 SQL Server 2014](../install-windows/install-sql-server-from-the-command-prompt.md)。  
  
 <sup>2</sup>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务的实例上禁用[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]和[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]具有高级服务。  
  
###  <a name="Firewall"></a> 防火墙端口  
 在大多数情况下，首次安装时，可以通过与 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 安装在相同计算机上的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 等此类工具连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不会在 Windows 防火墙中打开端口。 在将 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置为侦听 TCP 端口，并且在 Windows 防火墙中打开适当的端口进行连接之前，将无法从其他计算机建立连接。 有关详细信息，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
##  <a name="Serv_Perm"></a> 服务权限  
 此部分介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的 Per-service SID 配置的权限。  
  
-   [服务配置和访问控制](#Serv_SID)  
  
-   [Windows 特权和权限](#Windows)  
  
-   [授予 SQL Server Per-service SID 或 SQL Server 本地 Windows 组的文件系统权限](#Reviewing_ACLs)  
  
-   [授予其他 Windows 用户帐户或组的文件系统权限](#File_System_Other)  
  
-   [与非寻常磁盘位置相关的文件系统权限](#Unusual_Locations)  
  
-   [查看其他注意事项](#Review_additional_considerations)  
  
-   [注册表权限](#Registry)  
  
-   [WMI](#WMI)  
  
-   [命名管道](#Pipes)  
  
###  <a name="Serv_SID"></a> 服务配置和访问控制  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 会为其每项服务启用 Per-service SID，以提供深层服务隔离与防御。 Per-service SID 从服务名称派生得到，对该服务是唯一的。 例如，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务的服务 SID 名称可能是 **NT Service\MSSQL$**_\<InstanceName>_。 通过服务隔离，可直接访问特定的对象，而无需运行高特权帐户，也不会削弱为对象提供的安全保护水平。 通过使用包含服务 SID 的访问控制项， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务可限制对其资源的访问。  
  
> [!NOTE]  
>  在 Windows 7 和 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2（及更高版本）上，Per-service SID 可以是服务使用的虚拟帐户。  
  
 对于大多数组件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 直接为 Per-service 帐户配置 ACL，因此，无需重复资源 ACL 过程即可更改此服务帐户。  
  
 当安装 [!INCLUDE[ssAS](../../includes/ssas-md.md)]时，将创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务的 Per-service SID。 创建了本地 Windows 组，其命名格式为 **SQLServerMSASUser$**_computer_name_**$**_instance_name_。 Per-service SID **NT SERVICE\MSSQLServerOLAPService** 已被授予本地 Windows 组中的成员资格，而本地 Windows 组在 ACL 中被授予了适当的权限。 如果更改了用来启动 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务的帐户， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器必须更改某些 Windows 权限（如作为服务登录的权限），但分配给本地 Windows 组的权限将仍可用且没有任何更新，因为 Per-service SID 没发生变化。 此方法允许在升级过程中重命名 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序为 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务创建一个本地 Windows 组。 对于这些服务， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将为此本地 Windows 组配置 ACL。  
  
 在安装或升级期间，系统可能会将服务或服务 SID 的服务帐户添加为服务组的成员，具体取决于服务配置。  
  
###  <a name="Windows"></a> Windows 特权和权限  
 为启动服务分配的帐户需要对于服务的 **启动、停止和暂停权限** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将自动分配此权限。  首先，安装远程服务器管理工具 (RSAT)。 请参阅 [Remote Server Administration Tools for Windows 7](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=7d2f6ad7-656b-4313-a005-4e344e43997d)（Windows 7 的远程服务器管理工具）。  
  
 下表说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件使用的 Per-service SID 或本地 Windows 组请求的权限。  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序授予的权限|  
|---------------------------------------|------------------------------------------------------------|  
|**[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:**<br /><br /> （所有权限都将授予 Per-service SID。 默认实例：NT SERVICE\MSSQLSERVER。 命名的实例：NT SERVICE\MSSQL$InstanceName。）|**以服务身份登录** (SeServiceLogonRight)<br /><br /> **替换进程级别标记** (SeAssignPrimaryTokenPrivilege)<br /><br /> **跳过遍历检查** (SeChangeNotifyPrivilege)<br /><br /> **调整进程的内存配额** (SeIncreaseQuotaPrivilege)<br /><br /> 启动 SQL 编写器的权限<br /><br /> 读取事件日志服务的权限<br /><br /> 读取远程过程调用服务的权限|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理：**<sup>1</sup><br /><br /> （所有权限都将授予 Per-service SID。 默认实例：NT Service\SQLSERVERAGENT。 命名的实例：NT Service\SQLAGENT$InstanceName。）|**以服务身份登录** (SeServiceLogonRight)<br /><br /> **替换进程级别标记** (SeAssignPrimaryTokenPrivilege)<br /><br /> **跳过遍历检查** (SeChangeNotifyPrivilege)<br /><br /> **调整进程的内存配额** (SeIncreaseQuotaPrivilege)|  
|**[!INCLUDE[ssAS](../../includes/ssas-md.md)]:**<br /><br /> （所有权限都授予本地 Windows 组。 默认实例：SQLServerMSASUser$ComputerName$MSSQLSERVER。 命名的实例：SQLServerMSASUser$ComputerName$InstanceName。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 实例：SQLServerMSASUser$ComputerName$PowerPivot。）|**以服务身份登录** (SeServiceLogonRight)<br /><br /> 仅适用于表格：<br /><br /> **增加进程工作集** (SeIncreaseWorkingSetPrivilege)<br /><br /> **调整进程的内存配额** (SeIncreaseQuotaSizePrivilege)<br /><br /> “锁定内存页”(SeLockMemoryPrivilege) - 仅当完全关闭分页时才需要。<br /><br /> 仅适用于故障转移群集安装：<br /><br /> **提高计划优先级** (SeIncreaseBasePriorityPrivilege)|  
|**[!INCLUDE[ssRS](../../includes/ssrs.md)]:**<br /><br /> （所有权限都将授予 Per-service SID。 默认实例：NT SERVICE\ReportServer。 命名的实例：**NT SERVICE\\$**_InstanceName_。)|**以服务身份登录** (SeServiceLogonRight)|  
|**[!INCLUDE[ssIS](../../includes/ssis-md.md)]:**<br /><br /> （所有权限都将授予 Per-service SID。 默认实例和命名的实例：**NT SERVICE\MsDtsServer120**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 没有针对命名实例的单独进程。）|**以服务身份登录** (SeServiceLogonRight)<br /><br /> 应用程序事件日志的写入权限。<br /><br /> **跳过遍历检查** (SeChangeNotifyPrivilege)<br /><br /> **身份验证后模拟客户端** (SeImpersonatePrivilege)|  
|**全文搜索：**<br /><br /> （所有权限都将授予 Per-service SID。 默认实例：NT Service\MSSQLFDLauncher。 命名的实例：NT Service\ MSSQLFDLauncher$InstanceName。）|**以服务身份登录** (SeServiceLogonRight)<br /><br /> **调整进程的内存配额** (SeIncreaseQuotaPrivilege)<br /><br /> **跳过遍历检查** (SeChangeNotifyPrivilege)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser：**<br /><br /> （所有权限都授予本地 Windows 组。 默认实例或命名的实例：SQLServer2005SQLBrowserUser$ComputerName。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 没有针对命名实例的单独进程。）|**以服务身份登录** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 编写器：**<br /><br /> （所有权限都将授予 Per-service SID。 默认实例或命名的实例：NT Service\SQLWriter。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 编写器没有针对命名实例的单独进程。）|SQLWriter 服务在具有所需的所有权限的 LOCAL SYSTEM 帐户下运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不检查此服务或为其授予权限。|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 控制器：**|**以服务身份登录** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 客户端：**|**以服务身份登录** (SeServiceLogonRight)|  
  
 <sup>1</sup>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务的实例上禁用[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。  
  
###  <a name="Reviewing_ACLs"></a> 授予 SQL Server Per-service SID 或本地 Windows 组的文件系统权限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户必须具有对资源的访问权限。 为 Per-service SID 或本地 Windows 组设置了访问控制列表。  
  
> [!IMPORTANT]  
>  对于故障转移群集安装，必须为本地帐户的 ACL 设置共享磁盘上的资源。  
  
 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序设置的 ACL：  
  
|服务帐户针对|文件和文件夹|访问|  
|-------------------------|-----------------------|------------|  
|MSSQLServer|Instid\MSSQL\backup|完全控制|  
||Instid\MSSQL\binn|读取和执行|  
||Instid\MSSQL\data|完全控制|  
||Instid\MSSQL\FTData|完全控制|  
||Instid\MSSQL\Install|读取和执行|  
||Instid\MSSQL\Log|完全控制|  
||Instid\MSSQL\Repldata|完全控制|  
||120\shared|读取和执行|  
||Instid\MSSQL\Template Data（仅限[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] ）|读取|  
|SQLServerAgent<sup>1</sup>|Instid\MSSQL\binn|完全控制|  
||Instid\MSSQL\binn|完全控制|  
||Instid\MSSQL\Log|读取、写入、删除和执行|  
||120\com|读取和执行|  
||120\shared|读取和执行|  
||120\shared\Errordumps|读取和写入|  
||ServerName\EventLog|完全控制|  
|FTS|Instid\MSSQL\FTData|完全控制|  
||Instid\MSSQL\FTRef|读取和执行|  
||120\shared|读取和执行|  
||120\shared\Errordumps|读取和写入|  
||Instid\MSSQL\Install|读取和执行|  
||Instid\MSSQL\jobs|读取和写入|  
|MSSQLServerOLAPService|120\shared\ASConfig|完全控制|  
||Instid\OLAP|读取和执行|  
||Instid\Olap\Data|完全控制|  
||Instid\Olap\Log|读取和写入|  
||Instid\OLAP\Backup|读取和写入|  
||Instid\OLAP\Temp|读取和写入|  
||120\shared\Errordumps|读取和写入|  
|SQLServerReportServerUser|Instid\Reporting Services\Log Files|读取、写入、删除|  
||Instid\Reporting Services\ReportServer|读取和执行|  
||Instid\Reportingservices\Reportserver\global.asax|完全控制|  
||Instid\Reportingservices\Reportserver\Reportserver.config|读取|  
||Instid\Reporting Services\reportManager|读取和执行|  
||Instid\Reporting Services\RSTempfiles|读取、写入、执行、删除|  
||120\shared|读取和执行|  
||120\shared\Errordumps|读取和写入|  
|MSDTSServer100|120\dts\binn\MsDtsSrvr.ini.xml|读取|  
||120\dts\binn|读取和执行|  
||120\shared|读取和执行|  
||120\shared\Errordumps|读取和写入|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|120\shared\ASConfig|读取|  
||120\shared|读取和执行|  
||120\shared\Errordumps|读取和写入|  
|SQLWriter|不适用（以 Local System 身份运行）||  
|“用户”|Instid\MSSQL\binn|读取和执行|  
||Instid\Reporting Services\ReportServer|读取、执行和列出文件夹内容|  
||Instid\Reportingservices\Reportserver\global.asax|读取|  
||Instid\Reporting Services\reportManager|读取和执行|  
||Instid\Reporting Services\ReportManager\pages|读取|  
||Instid\Reporting Services\ReportManager\Styles|读取|  
||120\dts|读取和执行|  
||120\tools|读取和执行|  
||100\tools|读取和执行|  
||90\tools|读取和执行|  
||80\tools|读取和执行|  
||120\sdk|读取|  
||Microsoft SQL Server\120\Setup Bootstrap|读取和执行|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 控制器|\<ToolsDir>\DReplayController\Log\（空目录）|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayController\DReplayController.exe|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayController\resources\| 读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayController\\{all dlls}|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayController\DReplayController.config|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayController\IRTemplate.tdf|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayController\IRDefinition.xml|读取、执行和列出文件夹内容|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 客户端|\<ToolsDir>\DReplayClient\Log\| 读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayClient\DReplayClient.exe|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayClient\resources\| 读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayClient\ (all dlls)|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayClient\DReplayClient.config|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayClient\IRTemplate.tdf|读取、执行和列出文件夹内容|  
||\<ToolsDir>\DReplayClient\IRDefinition.xml|读取、执行和列出文件夹内容|  
  
 <sup>1</sup>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务的实例上禁用[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]和[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]具有高级服务。  
  
 当数据库文件存储在用户定义的位置时，您必须授予每个服务 SID 访问该位置的权限。 有关将文件系统权限授予 Per-service SID 的详细信息，请参阅 [配置数据库引擎访问的文件系统权限](configure-file-system-permissions-for-database-engine-access.md)。  
  
###  <a name="File_System_Other"></a> 授予其他 Windows 用户帐户或组的文件系统权限  
 可能还必须向内置帐户或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户授予某些访问控制权限。 下表列出了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序设置的其他 ACL。  
  
|请求组件|帐户|资源|权限|  
|--------------------------|-------------|--------------|-----------------|  
|MSSQLServer|性能日志用户|Instid\MSSQL\binn|列出文件夹内容|  
||性能监视器用户|Instid\MSSQL\binn|列出文件夹内容|  
||性能日志用户、性能监视器用户|\WINNT\system32\sqlctr120.dll|读取和执行|  
||仅限于管理员|\\\\.\root\Microsoft\SqlServer\ServerEvents\\<sql_instance_name><sup>1</sup>|完全控制|  
||管理员和系统|\tools\binn\schemas\sqlserver\2004\07\showplan|完全控制|  
||用户|\tools\binn\schemas\sqlserver\2004\07\showplan|读取和执行|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|\<报表服务器 Web 服务帐户>|\<install>\Reporting Services\LogFiles|DELETE<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||报表管理器应用程序池标识、 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帐户、Everyone|*\<install>* \Reporting Services\ReportManager, *\<install>* \Reporting Services\ReportManager\Pages\\\*.\*, *\<install>* \Reporting Services\ReportManager\Styles\\\*.\*, *\<install>* \Reporting Services\ReportManager\webctrl_client\1_0\\*。\*|读取|  
||报表管理器应用程序池标识|*\<install>* \Reporting Services\ReportManager\Pages\\*。\*|读取|  
||\<报表服务器 Web 服务帐户>|\<install>\Reporting Services\ReportServer|读取|  
||\<报表服务器 Web 服务帐户>|\<install>\Reporting Services\ReportServer\global.asax|完全|  
||Everyone|\<install>\Reporting Services\ReportServer\global.asax|READ_CONTROL<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_READ_ATTRIBUTES|  
||NETWORK SERVICE|\<install>\Reporting Services\ReportServer\ReportService.asmx|完全|  
||Everyone|\<install>\Reporting Services\ReportServer\ReportService.asmx|READ_CONTROL<br /><br /> SYNCHRONIZE FILE_GENERIC_READ<br /><br /> FILE_GENERIC_EXECUTE<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_EXECUTE<br /><br /> FILE_READ_ATTRIBUTES|  
||ReportServer Windows 服务帐户|\<install>\Reporting Services\ReportServer\RSReportServer.config|DELETE<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Everyone|报表服务器密钥（Instid 配置单元）|查询值<br /><br /> 枚举子项<br /><br /> 通知<br /><br /> 读取控制|  
||终端服务用户|报表服务器密钥（Instid 配置单元）|查询值<br /><br /> 设置值<br /><br /> 创建子项<br /><br /> 枚举子项<br /><br /> 通知<br /><br /> DELETE<br /><br /> 读取控制|  
||超级用户|报表服务器密钥（Instid 配置单元）|查询值<br /><br /> 设置值<br /><br /> 创建子项<br /><br /> 枚举子项<br /><br /> 通知<br /><br /> DELETE<br /><br /> 读取控制|  
  
 <sup>1</sup>这是 WMI 提供程序命名空间。  
  
###  <a name="Unusual_Locations"></a> 与非寻常磁盘位置相关的文件系统权限  
 当安装 tempdb 或用户数据库时，默认的安装位置驱动器为 **systemdrive**，通常是驱动器 C。  
  
 **非默认的驱动器**  
  
 当安装到不是默认驱动器的本地驱动器时，Per-service SID 必须对文件位置具有访问权限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将预配所需的访问权限。  
  
 **网络共享**  
  
 当数据库安装到网络共享时，服务帐户必须对用户数据库和 tempdb 数据库的文件位置具有访问权限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序无法设置对于网络共享的访问权限。 用户必须为服务帐户设置对 tempdb 位置的访问权限，然后才能运行安装程序。 用户必须设置对用户数据库位置的访问权限，然后才能创建数据库。  
  
> [!NOTE]  
>  虚拟帐户无法通过身份验证，因而无法访问远程位置。 所有虚拟帐户均使用计算机帐户的权限。 以 _<domain_name>_**\\**_<computer_name>_**$** 格式设置计算机帐户。  
  
###  <a name="Review_additional_considerations"></a>查看其他注意事项  
 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务提供其他功能时所需的权限：  
  
|服务/应用程序|功能|必需的权限|  
|--------------------------|-------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|使用 xp_sendmail 写入邮件槽。|网络写入权限。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|运行用户的而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员的 xp_cmdshell。|充当操作系统的一部分以及替换进程级别标记。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理 (MSSQLSERVER)|使用自动重新启动功能。|必须是本地 Administrators 组的成员。|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问|优化数据库以获得最佳查询性能。|第一次使用时，拥有系统管理员权限的用户必须初始化该应用程序。 初始化后，dbo 用户可使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 优化顾问仅优化他们拥有的那些表。 有关详细信息，请参阅 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 联机丛书中的“在第一次使用时初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 优化顾问”。|  
  
> [!IMPORTANT]  
>  升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请先为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启用 Windows 身份验证，并验证所需的默认配置： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务帐户是否为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin 组的成员。  
  
###  <a name="Registry"></a>注册表权限  
 将在 **HKLM\Software\Microsoft\Microsoft SQL Server\\**_<Instance_ID>_ 下为识别实例的组件创建注册表配置单元。 例如：  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL12.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSASSQL12.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL.120**  
  
 注册表还维护实例 ID 到实例名的映射。 实例 ID 到实例名的映射按如下方式维护：  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\SQL] "InstanceName"="MSSQL12"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\OLAP] "InstanceName"="MSASSQL12"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\RS] "InstanceName"="MSRSSQL12"**  
  
###  <a name="WMI"></a> WMI  
 Windows Management Instrumentation (WMI) 必须能够连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 为了支持这一点，需在**中预配 Windows WMI 提供程序 (** NT SERVICE\winmgmt [!INCLUDE[ssDE](../../includes/ssde-md.md)]) 的 per-service SID。  
  
 SQL WMI 提供程序需要以下权限：  
  
-   msdb 数据库的 **db_ddladmin** 或 **db_owner** 固定服务器角色中的成员资格。  
  
-   服务器中的**CREATE DDL EVENT NOTIFICATION** 权限。  
  
-   **中的** CREATE TRACE EVENT NOTIFICATION [!INCLUDE[ssDE](../../includes/ssde-md.md)]权限。  
  
-   **VIEW ANY DATABASE** 服务器级别权限。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会创建一个 SQL WMI 命名空间，并向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务 SID 授予读取权限。  
  
###  <a name="Pipes"></a> 命名管道  
 在所有安装中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序都通过共享内存协议（这是一种本地命名管道）提供针对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的访问权限。  
  
##  <a name="Provisioning"></a> 预配  
 此部分介绍如何在各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件内设置帐户。  
  
-   [数据库引擎预配](#DE_Prov)  
  
    -   [Windows 主体](#Win_Principals)  
  
    -   [sa 帐户](#sa)  
  
    -   [SQL Server Per-service SID 登录名和特权](#Logins)  
  
    -   [SQL Server 代理登录名和特权](#Agent)  
  
    -   [HADRON 和 SQL 故障转移群集实例和特权](#Hadron)  
  
    -   [SQL 编写器和特权](#Writer)  
  
    -   [SQL WMI 和特权](#SQLWMI)  
  
-   [SSAS 预配](#SSAS)  
  
-   [SSRS 预配](#SSRS)  
  
###  <a name="DE_Prov"></a> 数据库引擎预配  
 以下帐户将作为登录名添加到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中。  
  
####  <a name="Win_Principals"></a> Windows 主体  
 在安装过程中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序要求至少将一个用户帐户命名为 **sysadmin** 固定服务器角色的成员。  
  
####  <a name="sa"></a> sa 帐户  
 **sa** 帐户始终作为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 登录名存在，它是 **sysadmin** 固定服务器角色的成员。 当仅使用 Windows 身份验证安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 时（也即，当未启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时）， **sa** 登录名仍然存在，但处于禁用状态。 有关启用 **sa** 帐户的信息，请参阅 [更改服务器身份验证模式](change-server-authentication-mode.md)。  
  
####  <a name="Logins"></a> SQL Server Per-service SID 登录名和特权  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的 Per-service SID 设置为一个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 登录名。 Per-service SID 登录名是 **sysadmin** 固定服务器角色的成员。  
  
####  <a name="Agent"></a> SQL Server 代理登录名和特权  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务的 Per-service SID 设置为一个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 登录名。 Per-service SID 登录名是 **sysadmin** 固定服务器角色的成员。  
  
####  <a name="Hadron"></a>[!INCLUDE[ssHADRc](../../includes/sshadrc-md.md)] 和 SQL 故障转移群集实例和特权  
 当将 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 安装为 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 或 SQL 故障转移群集实例 (SQL FCI) 时，将在 **中设置** LOCAL SYSTEM [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 **LOCAL SYSTEM** 登录名被授予 **ALTER ANY AVAILABILITY GROUP** 权限（对于 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]）以及 **VIEW SERVER STATE** 权限（对于 SQL FCI）。  
  
####  <a name="Writer"></a> SQL 编写器和特权  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 编写器服务的 Per-service SID 设置为一个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 登录名。 Per-service SID 登录名是 **sysadmin** 固定服务器角色的成员。  
  
####  <a name="SQLWMI"></a> SQL WMI 和特权  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将 **NT SERVICE\Winmgmt** 帐户设置为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 登录名，并将其添加到 **sysadmin** 固定服务器角色中。  
  
#### <a name="ssrs-provisioning"></a>SSRS 预配  
 在安装过程中指定的帐户将设置为 **RSExecRole** 数据库角色的成员。 有关详细信息，请参阅 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
###  <a name="SSAS"></a>SSAS 预配  
 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 服务帐户要求各不相同，具体取决于服务器的部署方式。 如果您正在安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会要求您将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务配置在域帐户下运行。 为了支持 SharePoint 中内置的托管帐户功能，需要域帐户。 为此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序没有为 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装提供默认服务帐户，如虚拟帐户。 有关设置 PowerPivot for SharePoint 的详细信息，请参阅[配置 PowerPivot 服务帐户](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)。  
  
 对于所有其他独立 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 安装，您可以将服务设置为在域帐户、内置系统帐户、托管帐户或虚拟帐户下运行。 有关帐户设置的详细信息，请参阅[配置服务帐户 (Analysis Services)](../../analysis-services/instances/configure-service-accounts-analysis-services.md)。  
  
 对于群集安装，您必须指定一个域帐户或一个内置系统帐户。 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 故障转移群集既不支持托管帐户，也不支持虚拟帐户。  
  
 所有 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 安装均要求您指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的系统管理员。 管理员特权在 Analysis Services 的 **“服务器”** 角色中设置。  
  
###  <a name="SSRS"></a> SSRS 预配  
 在安装过程中指定的帐户将在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中设置为 **RSExecRole** 数据库角色的成员。 有关详细信息，请参阅 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
##  <a name="Upgrade"></a>从早期版本升级  
 此部分介绍在从先前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]升级的过程中进行的更改。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 要求 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 SP1、Windows Server 2012、Windows 8.0、Windows Server 2012 R2 或 Windows 8.1。 任何在更低操作系统版本上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 先前版本在升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，都必须升级操作系统。  
  
-   在将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的过程中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将按以下方式配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用 Per-service SID 的安全上下文运行。 将向 Per-service SID 授予针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的文件夹（如 DATA）和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 注册表项的访问权限。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 Per-service SID 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中设置为 **sysadmin** 固定服务器角色的成员。  
  
    -   Per-service SID 将添加到本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 组中，除非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是故障转移群集实例。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源保持设置为本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 组。  
  
    -   服务的本地 Windows 组已从 **SQLServer2005MSSQLUser$**_<computer_name>_**$**_<instance_name>_ 重命名为 **SQLServerMSSQLUser$**_<computer_name>_**$**_<instance_name>_。 已迁移的数据库的文件位置将具有本地 Windows 组的访问控制项 (ACE)。 新数据库的文件位置将具有 Per-service SID 的 ACE。  
  
-   从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 进行升级的过程中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将保留 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Per-service SID 的 ACE。  
  
-   对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例，将保留为服务配置的域帐户的 ACE。  
  
##  <a name="Appendix"></a> 附录  
 本节包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他信息。  
  
-   [服务帐户的描述](#Serv_Accts)  
  
-   [辨别识别实例的服务和不识别实例的服务](#Identify_instance_aware_and_unaware)  
  
-   [本地化的服务名称](#Localized_service_names)  
  
###  <a name="Serv_Accts"></a> 服务帐户的描述  
 服务帐户是用来启动 Windows 服务的帐户，如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。  
  
####  <a name="Any_OS"></a> 可用于任何操作系统的帐户  
 除了前面介绍的新的 [MSA](#MSA) 和 [虚拟帐户](#VA_Desc) 之外，还可以使用以下帐户。  
  
 <a name="Domain_User"></a>**Domain User 帐户**  
  
 如果服务必须与网络服务进行交互，则访问类似于文件共享的域资源；如果服务使用到运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他计算机的链接服务器连接，则可以使用具有最低特权的域帐户。 许多服务器到服务器的活动只能使用域用户帐户来执行。 此帐户应由域管理员在您的环境内预先创建。  
  
> [!NOTE]  
>  如果您将应用程序配置为使用域帐户，则可以隔离应用程序的特权，但必须手动管理密码或创建自定义解决方案以管理这些密码。 许多服务器应用程序使用此策略以增强安全性，但此策略要求额外的管理和复杂性。 在这些部署中，服务管理员将在维护任务方面花费大量时间，如管理服务密码和服务主体名称 (SPN)，但这些维护服务是 Kerberos 身份验证所必需的。 此外，这些维护任务可能会中断服务。  
  
 <a name="Local_User"></a> **Local User Accounts**  
  
 如果计算机不在域中，则建议您使用不具有 Windows 管理员权限的本地用户帐户。  
  
 <a name="Local_Service"></a>**Local Service 帐户**  
  
 Local Service 帐户是一个内置帐户，与 Users 组的成员具有相同级别的资源和对象访问权限。 如果有个别服务或进程的安全性受到威胁，则此有限访问权限有助于保护系统的安全性。 以 Local Service 帐户身份运行的服务将以一个没有凭据的 Null 会话形式访问网络资源。 请注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务不支持 Local Service 帐户。 不支持将 Local Service 作为运行这些服务的帐户，因为该服务是一个共享服务，并且任何在 Local Service 下运行的其他服务都对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有系统管理员访问权限。 该帐户的实际名称为 **NT AUTHORITY\LOCAL SERVICE**。  
  
 <a name="Network_Service"></a>**Network Service 帐户**  
  
 Network Service 帐户是一个内置帐户，比 Users 组的成员拥有更多的对资源和对象的访问权限。 以网络服务帐户身份运行的服务通过使用计算机帐户的凭据（格式为 _<domain_name>_**\\**_<computer_name>_**$**）访问网络资源。 该帐户的实际名称为 **NT AUTHORITY\NETWORK SERVICE**。  
  
 <a name="Local_System"></a>**Local System 帐户**  
  
 Local System 是一个具有高特权的内置帐户。 它对本地系统拥有许多特权并作为网络上的计算机。 该帐户的实际名称为 **NT AUTHORITY\SYSTEM**。  
  
###  <a name="Identify_instance_aware_and_unaware"></a> 辨别识别实例的服务和不识别实例的服务  
 识别实例的服务与特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例相关联，并具有自己的注册表配置单元。 通过为每个组件或服务运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序，可以安装识别实例的服务的多个副本。 不识别实例的服务由所有已安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例共享。 它们不与特定实例相关联，仅安装一次且不能并行安装。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中识别实例的服务包括：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理  
  
     请注意，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services 实例上 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 代理服务已禁用。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] <sup>1</sup>  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   全文搜索  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不识别实例的服务包括：  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
  
-   SQL 编写器  
  
 <sup>1</sup>在 SharePoint 集成模式下的 analysis Services 作为单个命名实例运行作为 PowerPivot。 实例名称是固定不变的。 您不能指定其他名称。 您可以在每台物理服务器上安装作为 PowerPivot 运行的一个 Analysis Services 实例。  
  
###  <a name="Localized_service_names"></a> 本地化的服务名称  
 下表列出了 Windows 的本地化版本所显示的服务名称。  
  
|语言|Local Service 的名称|Network Service 的名称|Local System 的名称|Admin Group 的名称|  
|--------------|----------------------------|------------------------------|---------------------------|--------------------------|  
|英语<br /><br /> 简体中文<br /><br /> 繁体中文<br /><br /> 朝鲜语<br /><br /> 日语|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|德语|NT-AUTORITÄT\LOKALER DIENST|NT-AUTORITÄT\NETZWERKDIENST|NT-AUTORITÄT\SYSTEM|VORDEFINIERT\Administratoren|  
|法语|AUTORITE NT\SERVICE LOCAL|AUTORITE NT\SERVICE RÉAU|AUTORITE NT\SYSTEM|BUILTIN\Administrators|  
|意大利语|NT AUTHORITY\SERVIZIO LOCALE|NT AUTHORITY\SERVIZIO DI RETE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|西班牙语|NT AUTHORITY\SERVICIO LOC|NT AUTHORITY\SERVICIO DE RED|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|俄语|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Администраторы|  
  
## <a name="related-content"></a>相关内容  
 [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [SQL Server 的默认实例和命名实例的文件位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  