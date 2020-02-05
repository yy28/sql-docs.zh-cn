---
title: 初始化报表服务器（SSRS 配置管理器）| Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8fdb68c0e61d5b48db3a997af0315e7cabf302f6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "73593547"
---
# <a name="ssrs-encryption-keys---initialize-a-report-server"></a>SSRS 加密密钥 - 初始化报表服务器
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，已初始化的服务器是指可以在报表服务器数据库中加密和解密数据的服务器。 初始化是一项必需的报表服务器操作。 初始化在报表服务器服务第一次启动时发生。 在将报表服务器联接到现有部署，或在恢复进程中手动重新创建密钥时也需要进行初始化。 有关使用加密密钥的方法和原因的详细信息，请参阅[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)和[存储加密的报表服务器数据（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)。  
  
 加密密钥部分基于报表服务器服务的配置文件信息。 如果更改用于运行报表服务器服务的用户标识，则必须相应地更新密钥。 如果使用 Reporting Services 配置工具更改标识，将自动处理此步骤。  
  
 如果由于某些原因导致初始化失败，则报表服务器在响应用户和服务请求时将返回 **RSReportServerNotActivated** 错误。 这种情况下，可能需要排除系统或服务器配置故障。 有关详细信息，请参阅 Technet Wiki 中的 [SSRS：解决 Reporting Services 的问题和错误](https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) 。  
  
## <a name="overview-of-the-initialization-process"></a>初始化过程概述  
 初始化过程将创建并存储一个用于加密的对称密钥。 对称密钥由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 加密服务创建，随后由报表服务器服务用来加密和解密数据。 对称密钥本身通过非对称密钥进行加密。  
  
 以下步骤描述了初始化过程：  
  
1.  在初始启动时，报表服务器服务读取 RSReportServer.config 文件以获取安装标识符和数据库连接信息。  
  
2.  报表服务器服务从加密服务请求公钥。 Windows 创建私钥和公钥并将公钥发送到报表服务器服务。  
  
3.  报表服务器服务连接到报表服务器数据库并存储安装标识符和公钥值。  
  
4.  报表服务器服务再次调入加密服务，这次是请求对称密钥。 Windows 创建对称密钥。  
  
5.  报表服务器服务再次连接到报表服务器数据库，并将对称密钥添加到步骤 3 中存储的公钥和安装标识符值中。 在存储对称密钥之前，报表服务器服务使用其公钥对对称密钥进行加密。 存储对称密钥后，即可将报表服务器视为已初始化，并且可供使用。  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>针对扩展部署初始化报表服务器  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持在多个报表服务器实例中共享单个报表服务器数据库的扩展部署模型。 若要联接扩展部署，报表服务器必须在共享数据库中创建并存储其对称密钥副本。 尽管使用该数据库的服务器都使用同一个对称密钥，但是每个报表服务器都有自己的密钥副本。 每个副本各不相同，因为这些副本都使用其各自拥有的公钥进行了唯一加密。  
  
 针对扩展部署初始化报表服务器的开始步骤与描述初始化单个服务器和数据库组合的前三个步骤相同。  
  
 扩展部署初始化过程的不同之处在于报表服务器获取对称密钥的方式。 在初始化第一个服务器时，它从 Windows 获取对称密钥。 在配置扩展部署的过程中，在初始化第二个服务器时，它将从已初始化的报表服务器服务中获取对称密钥。 第一个报表服务器实例使用第二个实例的公钥来为第二个报表服务器实例创建对称密钥的加密副本。 在此过程中的任何一点，对称密钥永远不会作为纯文本公开。  
  
## <a name="how-to-initialize-a-report-server"></a>如何初始化报表服务器  
  
-   若要初始化报表服务器，请使用 Reporting Services 配置工具。 在创建和配置报表服务器数据库时，将自动进行初始化。 有关详细信息，请参阅 [配置报表服务器数据库连接（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)中支持的版本。  
  
-   若要针对扩展部署初始化报表服务器，可以使用 Reporting Services 配置工具中的“初始化”页或使用 **RSKeymgmt** 实用工具。 要按照分步说明操作，请参阅[配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
> [!NOTE]  
>  RSKeymgmt 是一种控制台应用程序，需要在托管扩展部署中已包含的报表服务器实例的计算机上从命令行运行  。 运行该实用工具时，需要指定相关参数，以选择要初始化的远程报表服务器实例。  
  
 只有当安装标识符与公钥相匹配时，才会初始化报表服务器。 如果匹配成功，则创建允许可逆加密的对称密钥。 如果匹配失败，则将禁用报表服务器，在这种情况下，可能需要应用备份密钥；如果备份密钥不可用或无效，则可能需要删除加密数据。 有关报表服务器使用的加密密钥的详细信息，请参阅[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。  
  
> [!NOTE]  
>  还可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows Management Instrumentation (WMI) 提供程序以编程的方式初始化报表服务器。 有关详细信息，请参阅 [访问 Reporting Services WMI 提供程序](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)。  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>如何确认报表服务器初始化  
 要确认报表服务器初始化，请通过在命令窗口中键入 https://**servername>/reportserver 来对报表服务器 Web 服务运行 ping 命令\<** 。 如果发生 **RSReportServerNotActivated** 错误，则表示初始化失败。  
  
## <a name="see-also"></a>另请参阅
[配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)
  
  
