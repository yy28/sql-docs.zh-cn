---
title: 安装 Distributed 的 Replay （安装程序） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0f9d81920e9e14dc745813795bcf98eb1d9ebdf9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051394"
---
# <a name="install-distributed-replay-setup"></a>安装 Distributed Replay（安装程序）
  使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Distributed Replay 功能。 在计划安装这些功能的位置时，请考虑以下方面：  
  
-   您可以将管理工具与 Distributed Replay 控制器安装在同一台计算机上，也可以安装在不同的计算机上。  
  
-   在每个 Distributed Replay 环境中只能有一个控制器。  
  
-   您可以将客户端服务最多安装在 16 个（物理或虚拟）计算机上。  
  
-   只能有客户端服务的一个实例安装在 Distributed Replay 控制器计算机上。 如果您的 Distributed Replay 环境将具有多个客户端，我们建议不要将客户端服务与该控制器安装在同一台计算机上。 这样做可能会降低 Distributed Replay 的整体速度。  
  
-   对于性能测试方案，我们建议不要将管理工具、分布式重播实用工具控制器服务或客户端服务安装在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目标实例上。 在目标服务器上安装所有这些功能应限于应用程序兼容性功能测试。  
  
-   在安装后，控制器服务（即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 控制器）必须首先运行，然后才能在客户端启动 Distributed Replay 客户端服务。  
  
> [!NOTE]  
>  若要删除或更改 Distributed Replay 功能，请使用 **“控制面板”** 中的 Windows **“程序和功能”** 窗口。 在“卸载或更改程序” [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 窗口中选择  ，然后单击 **“删除”** 以便打开 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。 在 **“选择功能”** 页上，选中要删除的 Distributed Replay 功能。  
  
 **先决条件：**  
  
-   请确保您要使用的计算机满足在 [Distributed Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)主题中介绍的要求。  
  
-   在开始此过程之前，请创建运行控制器和客户端服务所基于的域用户帐户。 我们建议这些帐户不是 Windows Administrators 组的成员。 有关详细信息，请参阅 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md) 主题中的“用户和服务帐户”部分。  
  
    > [!NOTE]  
    >  如果您在同一台计算机上运行管理工具、控制器服务和客户端服务，则可以使用本地用户帐户。  
  
 **安装位置：**  
  
 假定您在使用默认文件位置和标准安装，则基目录位于 C:\Program Files\Microsoft SQL Server。 其中，下面是二进制文件和程序集将安装到的位置：  
  
-   在 32 位系统上：  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]工具  
  
     \- 或 -  
  
     \<Share Feature Directory>\Tools\\（用户提供的替代共享功能目录）  
  
-   在 64 位系统上：  
  
     C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- 或 -  
  
     \<Share Feature Directory (x86)>\Tools\\（用户提供的替代共享功能 (x86) 目录）  
  
### <a name="to-install-distributed-replay-features"></a>安装 Distributed Replay 功能  
  
1.  若要开始安装任何 Distributed Replay 功能，请启动 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
2.  **“安装程序支持规则”** 页将标识在安装 SQL Server 安装程序支持文件时可能发生的问题。 在继续安装之前，您必须纠正任何安装程序支持问题。  
  
3.  在 **“产品密钥”** 页上，选择某一选项按钮，该按钮指示您是安装免费版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，还是安装具有 PID 密钥的产品的生产版本。 有关详细信息，请参阅[各版本和 SQL Server 2014 的组件](../editions-and-components-of-sql-server-2016.md)。  
  
4.  在 **“许可条款”** 页上阅读许可协议，然后选中相应的复选框以接受许可条款和条件。 为了帮助改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您还可以启用功能使用情况选项并将报告发送给 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
5.  在 **“安装程序支持文件”** 页，单击 **“安装”** 以便安装或更新 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的安装程序支持文件。  
  
6.  在 **“设置角色”** 页上，选择 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能安装”**，然后单击 **“下一步”** 以继续进入 **“功能选择”** 页。  
  
7.  在 **“功能选择”** 页上，配置要安装的功能。  
  
    -   若要安装管理工具，请选择“管理工具 - 基本”。  
  
    -   若要安装控制器服务，请选择 **“Distributed Replay 控制器”**。  
  
    -   若要安装客户端服务，请选择 **“Distributed Replay 客户端”**。  
  
     **重要**：在您配置 Distributed Replay 控制器时，可以指定将用于运行 Distributed Replay 客户端服务的一个或多个帐户。 下面是支持的帐户的列表：  
  
    -   域用户帐户  
  
    -   用户创建的本地用户帐户  
  
    -   管理员  
  
    -   虚拟帐户和 MSA（托管服务帐户）  
  
    -   Network Services、Local Services 和 System  
  
     不接受组帐户（本地或域）和其他内置帐户（如 Everyone）。  
  
8.  或者，单击省略号 (…) 按钮以便更改共享功能目录路径。  
  
    1.  在 32 位计算机上，默认安装路径为 **C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  在 64 位计算机上，默认安装路径为 C:\Program Files (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\  
  
9. 在完成后，单击 **“下一步”**。  
  
10. 在 **“安装规则”** 页上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将验证您的计算机配置。 在验证过程完成后，单击 **“下一步”**。  
  
11. **“磁盘空间要求”** 页计算指定的功能所需的磁盘空间， 然后将所需空间与可用磁盘空间进行比较。  
  
12. 在 **“错误报告”** 页上，指定要发送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 以帮助改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的信息。 默认情况下，将启用用于错误报告的选项。  
  
13. 在 **“安装配置规则”** 页上，系统配置检查器将运行多组规则来针对您指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能对您的计算机配置进行验证。  
  
14. 在 **“准备安装程序”** 页上，单击 **“安装”**。  
  
    > [!IMPORTANT]  
    >  安装 Distributed Replay 之后，您必须在控制器和客户端计算机上创建防火墙规则，并授予每台客户端计算机对目标服务器的权限。 有关详细信息，请参阅 [完成安装后步骤](../../tools/distributed-replay/complete-the-post-installation-steps.md)。  
  
 其他这些主题介绍了用于安装 Distributed Replay 的其他方法：  
  
-   [从命令提示符安装 Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [使用配置文件安装 Distributed Replay](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 您必须具有管理权限才能安装任何 Distributed Replay 功能。 只有拥有 sysadmin 权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名才可以将客户端服务帐户添加到测试服务器的 sysadmin 服务器角色中。 有关分布式重播的安全注意事项的详细信息，请参阅 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed 的 Replay 要求](../../tools/sql-server-profiler/replay-requirements.md)   
 [管理工具命令行选项（Distributed Replay 实用工具）](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [配置 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
