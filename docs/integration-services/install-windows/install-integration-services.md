---
title: "安装集成服务 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
caps.latest.revision: 106
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3e91abac8902868dc9edefc1466fb2d25a602462
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="install-integration-services"></a>安装集成服务
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了单个安装程序来安装其包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]在内的任一组件或所有组件。 通过安装程序，可在单台计算机上将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件一起安装，也可以单独安装。    
    
 本主题重点介绍在安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之前应了解的重要注意事项。 本主题中的信息将帮助您评估安装选项，以便您做出适当选择使安装成功完成。    
    
## <a name="preparing-to-install-integration-services"></a>准备安装 Integration Services    
 安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之前，请首先查看以下要求：    
    
-   [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [系统配置检查器的检查参数](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)    
    
-   [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="selecting-an-integration-services-configuration"></a>选择 Integration Services 配置    
 可以按下列配置安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ：    
    
-   你可以在没有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 先前实例的计算机上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。    
    
-   可以将 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 与 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 和 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]的现有实例并行安装。    
    
     当您在已安装了这些 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 早期版本之一的计算机上升级到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 时， [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 将与该早期版本并行安装。    
    
     有关升级的详细信息 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，请参阅 [升级集成服务](../../integration-services/install-windows/upgrade-integration-services.md)。 有关早期版本的向后兼容性详细信息， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]请参阅 [集成服务向后兼容性](../../integration-services/integration-services-backward-compatibility.md)。    
    
## <a name="installing-integration-services"></a>安装集成服务    
 在查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安装要求并确保计算机满足这些要求之后，就可以安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]了。    
    
> [!NOTE]    
>  在以前版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，在您安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 后，默认情况下 Users 组中的所有用户都已对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务具有访问权限。 在您安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时，用户无权访问 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。 该服务默认是安全的。 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员必须运行 DCOM 配置工具 (Dcomcnfg.exe) 以便授予特定用户对 **SQL Server Integration Services 13.0**的访问权限。    
>     
>  有关如何授予权限的说明，请参阅[Integration Services 服务 &#40;SSIS 服务 &#41;](../../integration-services/service/integration-services-service-ssis-service.md).    
    
 如果使用安装向导安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，则将使用一系列页面来指定组件和选项。 下表仅列出了安装向导中包含的选项在选中后会对 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]安装产生影响的页面：    
    
|第|建议|    
|----------|---------------------|    
|**功能选择**|选择 **集成服务** 可安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务并可在设计环境之外运行包。<br /><br /> 若要进行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]以及用于开发和管理包的工具和文档的完整安装，请同时选择 **集成服务** 及以下 **“共享功能”**：<br /><br /> -<br />                    **SQL Server Data Tools** ，以便安装用于设计包的工具。<br /><br /> -<br />                    **管理工具 – 完整** 以便安装 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用于管理包的工具。<br /><br /> -<br />                    **客户端工具 SDK** ，以便安装用于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 编程的托管程序集。<br /><br /> 很多数据仓库解决方案还要求安装其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件，例如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。<br /><br /> **在 64 位计算机上安装** 在 64 位计算机上安装，选择 **集成服务** ，则只安装 64 位运行时和工具。 如果必须以 32 位模式来运行包，还必须选择其他选项以安装 32 位运行时和工具：<br /><br /> 如果 64 位计算机运行的是 x86 操作系统，请选择 **SQL Server Data Tools** 或 **管理工具 - 完整**。<br /><br /> 如果 64 位计算机运行的是 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 操作系统，请选择 **管理工具 - 完整**。<br /><br /> **为 ETL 安装专用服务器** 若要对提取、转换和加载 (ETL) 过程使用专用服务器，建议你在安装 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 时安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的本地实例。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 通常将包存储在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中，并使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理对这些包进行计划。 如果 ETL 服务器上没有 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例，则必须通过具有 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的服务器计划或运行包。 这表示这些包不会在 ETL 服务器上运行，而是在其启动时所在的服务器上运行。 因此，专用 ETL 服务器的资源不会按预期方式使用。 而且，其他服务器的资源可能会受到 ETL 进程运行的影响<br /><br /> <br /><br /> 注意：如果选择了可在安装向导的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] “功能选择” **页上选择进行安装的某些** 组件，则会安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件的部分子集。 这些组件对特定任务是有用的，但 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能将受到限制。 例如， **“数据库引擎服务”** 选项将安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 导入和导出向导所需的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件。 **“SQL Server Data Tools”** 选项将安装在设计包时所需的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件，但不会安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，并且不能在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]之外运行包。 为确保完整安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，必须在 **“功能选择”** 页上选择“ **集成服务** ”。|    
|**实例配置**|在 **“实例配置”** 页上做出的任何选择都不会影响 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。<br /><br /> 在一台计算机上只能安装一个 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务实例。 可使用计算机名称连接到该服务。<br /><br /> 默认情况下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务将配置为管理存储在与 **同时安装的数据库引擎实例的** msdb [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]数据库中的包。 如果数据库引擎实例未与 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]同时安装，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务将配置为管理存储在本地默认 **实例的** msdb [!INCLUDE[ssDE](../../includes/ssde-md.md)]数据库中的包。 若要管理存储在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的某个命名实例或远程实例中的包或存储在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的多个实例中的包，必须修改配置文件。 有关如何修改此配置文件的详细信息，请参阅[Integration Services 服务 &#40;SSIS 服务 &#41;](../../integration-services/service/integration-services-service-ssis-service.md).|    
|**服务器配置**|在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] “服务器配置” **页的** “服务帐户” **选项卡上查看** 服务的设置。<br /><br /> 如果安装了 Windows 7 或 Windows Server 2008 R2，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务将注册为在 NT Services\MsDtsServer130 虚拟帐户下运行，并且 **启动类型** 为 **自动**。  您不必输入内置虚拟帐户的密码。 如果安装了 Microsoft Vista 或 Windows Server 2008，则 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务将注册为在内置网络服务帐户下运行，并且 **启动类型** 为 **自动**。 您不必输入内置 Network Service 帐户的密码。|    
    
 默认情况下，在全新安装中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 配置为不将与运行包相关的事件记录到应用程序事件日志中。 使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的数据收集器功能时，此设置可防止生成太多事件日志项。 未记录的事件包括 EventID 12288“包已启动”和 EventID 12289“包已成功完成”。 若要将这些事件记录到应用程序事件日志中，请打开注册表以进行编辑。 然后在注册表中，找到 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS 节点，并将 LogPackageExecutionToEventLog 设置的 DWORD 值从 0 更改为 1。    
    
## <a name="understanding-the-integration-services-service"></a>了解 Integration Services 服务    
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务。    
    
 如果在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] “功能选择” **页上选择“** 集成服务 **”选项，则会安装** 服务。 如果接受 **“服务器配置”** 页上的默认设置，则会启用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务，且 **“启动类型”** 为 **“自动”**。    
    
 在一台计算机上可以只安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务的一个实例。 该服务并不特定于具体的数据库引擎实例。 可使用运行该服务的计算机的名称连接到该服务。    
    
## <a name="installing-integration-services-on-64-bit-computers"></a>在 64 位计算机上安装 Integration Services    
    
### <a name="integration-services-features-installed-on-64-bit-computers"></a>安装在 64 位计算机上的 Integration Services 功能    
 安装程序将根据您选择的安装选项安装各种 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能：    
    
-   安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，如果选择安装 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，安装程序将安装所有可用的 64 位 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能和工具。    
    
-   如果需要 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 设计时功能，还必须安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。    
    
-   如果需要 32 位版本的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 运行时和工具，以便能以 32 位模式运行某些包，还必须安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。    
    
 64 位功能安装在 **Program Files** 目录下，而 32 位功能单独安装在 **Program Files (x86)** 目录下。 （这种行为并不特定于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）。    
    
> [!IMPORTANT]    
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 64 位操作系统不支持 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]（即 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 包的 32 位开发环境），因此不能将其安装在 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 服务器上。    
    
  

