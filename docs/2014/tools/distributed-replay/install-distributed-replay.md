---
title: 从命令提示符安装 Distributed 的 Replay |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67d74db6faf9b40ad323ed2948c2c0a596a63016
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149726"
---
# <a name="install-distributed-replay-from-the-command-prompt"></a>从命令提示符安装 Distributed Replay
  通过从命令提示符安装 Distributed Replay 的新实例，您可以指定要安装的功能以及如何配置这些功能。 在命令提示符下安装支持对 Distributed Replay 组件进行安装、修复、升级和卸载。 通过命令提示符安装时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持完全静默模式（通过使用 /Q 参数）。  
  
> [!NOTE]  
>  对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。  
  
## <a name="installation-parameters"></a>安装参数  
 顶级功能列表包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和工具。 工具功能将安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]和其他共享组件。 若要安装 Distributed Replay 组件，请指定以下参数：  
  
|组件|参数|  
|---------------|---------------|  
|“Distributed Replay 控制器”|**DREPLAY_CTLR**|  
|Distributed Replay 客户端|**DREPLAY_CLT**|  
|管理工具|**工具**|  
  
> [!IMPORTANT]  
>  安装 Distributed Replay 之后，您必须在控制器和客户端计算机上创建防火墙规则，并授予每台客户端计算机对目标服务器的权限。 有关详细信息，请参阅 [完成安装后步骤](complete-the-post-installation-steps.md)。  
  
 使用下表中的参数可开发用于安装的命令行脚本。  
  
|参数|Description|支持的值|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **可选**|Distributed Replay 控制器服务的服务帐户。|检查帐户和密码|  
|/CTLRSVCPASSWORD<br /><br /> **可选**|Distributed Replay 控制器服务帐户的密码。|检查帐户和密码|  
|/CTLRSTARTUPTYPE<br /><br /> **可选**|Distributed Replay 控制器服务的启动类型。|自动<br /><br /> 禁用<br /><br /> Manual|  
|/CTLRUSERS<br /><br /> **可选**|指定哪些用户对 Distributed Replay 控制器服务具有权限。|一组使用“ ”（空格）作为分隔符的用户帐户字符串<br /><br /> **重要**:当您配置 Distributed Replay 控制器服务时，可以指定将用于运行 Distributed Replay 客户端服务的一个或多个用户帐户。 下面是支持的帐户的列表：<br /><br /> 域用户帐户<br /><br /> 用户创建的本地用户帐户<br /><br /> 管理员<br /><br /> 虚拟帐户和 MSA（托管服务帐户）<br /><br /> Network Services、Local Services 和 System<br /><br /> <br /><br /> 不接受组帐户（本地或域）和其他内置帐户（如 Everyone）。|  
|/CLTSVCACCOUNT<br /><br /> **可选**|Distributed Replay 客户端服务的服务帐户。|检查帐户和密码|  
|/CLTSVCPASSWORD<br /><br /> **可选**|Distributed Replay 客户端服务帐户的密码。|检查帐户和密码|  
|/CLTSTARTUPTYPE<br /><br /> **可选**|Distributed Replay 客户端服务的启动类型。|自动<br /><br /> 禁用<br /><br /> Manual|  
|/CLTCTLRNAME<br /><br /> **可选**|客户端就 Distributed Replay 控制器服务与之通信的计算机的名称。||  
|/CLTWORKINGDIR<br /><br /> **可选**|Distributed Replay 客户端服务的工作目录。|有效的路径|  
|/CLTRESULTDIR<br /><br /> **可选**|Distributed Replay 客户端服务的结果目录。|有效的路径|  
  
### <a name="sample-syntax"></a>示例语法：  
 **安装 Distributed Replay 控制器组件**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **安装 Distributed Replay 客户端组件**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
  
