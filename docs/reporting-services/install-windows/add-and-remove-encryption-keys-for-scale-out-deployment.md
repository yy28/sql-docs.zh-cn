---
title: "添加和删除扩展部署的加密密钥 | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
caps.latest.revision: "10"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b7c90c1760c555f0099d9a6ea8fc675d0bd0719
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment"></a>添加和删除扩展部署的加密密钥
  通过将多个报表服务器配置为使用一个共享的报表服务器数据库，可以在扩展部署模型中运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 扩展部署中的成员身份是基于报表服务器是否将加密密钥存储在报表服务器数据库中。 通过为特定的报表服务器实例添加和删除加密密钥，可以控制扩展部署成员身份。 如果要从部署中删除节点，则可以按任意顺序进行删除。 如果要向部署中添加节点，则必须联接已作为部署的一部分的报表服务器中的所有新实例。  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>使用 Reporting Services 配置工具配置扩展部署  
 配置扩展部署的最简单方法是使用 Reporting Services 配置工具。 有关详细信息以及分步说明，请参阅[配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)。  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>使用 Rskeymgmt 配置扩展部署  
 使用 **rskeymgmt** 实用工具，可以将报表服务器实例初始化为使用共享的报表服务器数据库。 要向扩展部署中添加报表服务器，需要初始化报表服务器。 要进行初始化，需要有管理员权限。 对于承载要加入部署的报表服务器的远程计算机，您必须拥有管理员凭据。  
  
### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>如何将报表服务器加入扩展部署 (rskeymgmt)  
  
1.  在特定计算机的本地运行 **rskeymgmt.exe** ，该计算机承载已经是报表服务器扩展部署成员的报表服务器。  
  
2.  使用 **-j** 参数将报表服务器联接到报表服务器数据库。 使用 **-m** 和 **-n** 参数指定要添加到部署中的远程报表服务器实例。 使用 **-u** 和 **-v** 参数指定远程计算机上的管理员帐户。 如果要使用同一台计算机中的多个报表服务器实例创建扩展部署，则使用的语法会稍有不同。 有关应使用的语法的详细信息，请参阅 [rskeymgmt 实用工具 (SSRS)](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)。  
  
     下面的示例说明了将远程报表服务器加入扩展部署时必须指定的参数（如果您对远程计算机拥有管理员权限，则可以忽略凭据）：  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```
3. 重新启动 Reporting Services Windows 服务。
  
### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>如何从扩展部署 (rskeymgmt) 中删除报表服务器  
  
1.  打开要删除的报表服务器的 rsreportserver.config 文件，找到安装 ID。 默认情况下，此文件位于 Program Files\Microsoft SQL Server\MSSQL.*n*\Reporting Services\ReportServer)。  
  
     如果安装了单个实例，则计算机中只有一个 rsreportserver.config 文件。 如果安装了多个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例，则请使用 Reporting Services 配置工具中的“服务器状态”页来查找要删除的报表服务器的实例标识符（例如，MSSQL.2）。 为报表服务器实例存储程序文件的文件夹名称将基于实例标识符来命名（例如，Program Files\Microsoft SQL Server\MSSQL.2）。  
  
2.  运行 **rskeymgmt.exe**。 可以在属于报表服务器扩展部署一部分的任何报表服务器上运行该文件。  
  
3.  使用 **-r** 参数从扩展部署中释放该报表服务器实例。 下面的示例演示必须指定的参数：  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
4. 重新启动 Reporting Services Windows 服务。
  
 这些步骤从扩展部署中删除报表服务器，但不会卸载报表服务器上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。 从扩展部署中删除报表服务器之后，如果不再需要服务器上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，则可以卸载该服务器上的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 有关信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[卸载现有 SQL Server 实例（安装程序）](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)。  
  
## <a name="see-also"></a>另请参阅  
 [配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
