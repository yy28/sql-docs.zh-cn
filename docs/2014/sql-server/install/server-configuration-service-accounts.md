---
title: 服务器配置-服务帐户 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f642458f8d30fab0d20eeaad427831c5dece964
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659847"
---
# <a name="server-configuration---service-accounts"></a>服务器配置 - 服务帐户
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的“服务器配置”页可以为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务分配登录帐户。 此页上配置的实际服务取决于您选择安装的功能。  
  
 用于启动和运行的启动帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以是超链接"ms help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm"\l"Domain_User"域用户帐户、 本地用户帐户、 托管的服务帐户虚拟帐户或内置系统帐户。  
  
## <a name="options"></a>选项  
 您可以为所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务分配相同的登录帐户，也可以单独配置各个服务帐户。 您还可以指定是自动启动、手动启动还是禁用服务。 对于大多数安装建议采用默认帐户。  
  
 在 Windows 7 和 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 上，大多数帐户默认为虚拟帐户。  
  
 如果将服务配置为使用域帐户， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议对各服务帐户进行单独配置，以便为每项服务提供最低特权，即向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务授予它们完成各自任务所需的最低权限。 有关包含帐户类型的说明的详细信息，请参阅 [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
 **配置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]单独服务帐户 （推荐）**  
 使用网格为每项 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务设置一个登录用户名和密码并设置相应服务的启动类型。 您可以对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务使用内置系统帐户、本地帐户、本地组、域组或域用户帐户。  
  
 选择下列任一服务以自定义其设置。  
  
|选择此服务|为其配置身份验证设置的主体|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理|执行作业、监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并允许管理任务自动完成的服务。<br /><br /> 此服务没有默认登录帐户。<br /><br /> 默认的启动类型为“手动”。|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|默认的启动类型为“自动”。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|默认的启动类型为“自动”。<br /><br /> 对于 SharePoint 集成模式，您必须指定一个 Windows 域用户帐户。 您指定的帐户用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务。 您为当前实例指定的帐户还必须用于您以后添加到同一场的任何附加 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|服务帐户用于配置报表服务器数据库连接。 如果要使用默认的身份验证设置，请选择内置的网络服务。 如果指定域用户帐户，并且要在报表服务器上使用 Windows 身份验证，请确保为该帐户注册一个服务主体名称 (SPN)。 有关详细信息，请参阅 [Configure Windows Authentication on the Report Server](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)。<br /><br /> 默认的启动类型为“自动”。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是一组图形工具和可编程对象，用于移动、复制和转换数据。<br /><br /> 默认的启动类型为“自动”。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 客户端|用于 Distributed Replay 客户端服务的服务帐户。<br /><br /> 提供运行 Distributed Replay 客户端服务的帐户。 此帐户应该不同于用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户。<br /><br /> 默认的启动类型为“手动”。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 控制器|用于 Distributed Replay 控制器服务的服务帐户。<br /><br /> 提供运行 Distributed Replay 控制器服务的帐户。 此帐户应该不同于用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户。<br /><br /> 默认的启动类型为“手动”。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文筛选器后台程序启动器|创建 fdhost.exe 进程的服务。 需要使用此服务来承载为全文检索处理文本数据的断字符和筛选器。<br /><br /> 如果提供运行 FDHOST 启动器服务的域帐户，我们强烈建议您使用低特权的帐户。 此帐户应该不同于用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的帐户。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 是向客户端计算机提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接信息的名称解析服务。 多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 实例共享此服务。 默认的登录帐户为 NT Authority\Local service 且在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装期间无法更改。 可以在安装完成后更改该帐户。 如果未在安装期间指定启动类型，可以根据以下内容来确定：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 设置为“自动”并在下面描述的安装方案中运行：<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例<br />-<br />                            启用了 TCP 或 NP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例<br />-<br />                            Analysis Server 的命名实例，未进行群集<br /><br /> 如果上述方案均不符合并且已经安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser，将保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 的当前状态。<br /><br /> 如果在安装前没有现有的早期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的实例，则启动类型会设置为“已禁用”且被停止。|  
  
## <a name="see-also"></a>请参阅  
 [安装 SQL Server 的安全注意事项](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
