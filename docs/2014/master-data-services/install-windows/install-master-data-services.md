---
title: 安装 Master Data Services |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2645ae5b16ffa4738f06e1439abac977c8e18894
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479335"
---
# <a name="install-master-data-services"></a>安装 Master Data Services
  下面的流程图概要说明了如何安装并配置 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装过程包括三个部分：  
  
-   [预安装任务](#preinstall)：在安装前验证系统要求[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。  
  
-   [安装操作](#install):安装[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]通过使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装程序或命令提示符。  
  
-   [安装后任务](#postinstall)：打开[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]以完成安装后操作。 创建和配置 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序和 Web 服务并部署示例模型。  
  
##  <a name="preinstall"></a> 安装前任务  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|验证安装要求|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的计算机必须满足以下方面的最低要求：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。<br /><br /> [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序和 Web 服务。<br /><br /> [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库（如果数据库所在的计算机与 Web 应用程序所在的计算机相同）。<br /><br /> 请注意，您可以通过只在 web 服务器计算机上运行安装程序并创建单独的 web 服务器计算机和数据库服务器计算机[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]运行受支持的版本和版本的远程计算机上的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|[SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)<br /><br /> [安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Web 应用程序要求 (Master Data Services)](web-application-requirements-master-data-services.md)<br /><br /> [数据库要求 (Master Data Services)](database-requirements-master-data-services.md)|  
|配置所需的角色、角色服务和功能|运行安装程序前，请使用所需的 Windows 角色、角色服务和功能配置计算机。<br /><br /> 注意：尽管工作流的更高版本中，可以执行此步骤中，最好运行安装程序，因此，你可以执行紧挨安装后面的 web 配置任务前将此配置。|[Web 应用程序要求 (Master Data Services)](web-application-requirements-master-data-services.md)|  
|查看语言支持注意事项|确定要安装和运行 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 所用的语言。|[多语言和全球部署 (Master Data Services)](multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> 安装操作  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序|在将承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服务的计算机上，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序或命令提示符安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序时， [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 将显示在 **“功能选择”** 页上的 **“共享功能”** 下。 使用命令提示符时， [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 作为功能参数提供。 请注意，命令行安装过程将安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]，但不会对它进行配置。 您必须使用 Master Data Services 配置管理器对其进行配置。 安装过程：<br /><br /> 在您为共享功能指定的位置安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 文件夹和文件，并为这些对象分配权限。<br /><br /> 在全局程序集缓存 (GAC) 中注册 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 程序集。<br /><br /> 安装 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。|[从安装向导安装 SQL Server 2014&#40;安装程序&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [文件夹和文件权限 (Master Data Services)](../folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> 安装后任务  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 以便完成安装后操作|安装完成之后，打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 在本地计算机上执行以下安装后操作：<br /><br /> 创建一个 Windows 组 **MDS_ServiceAccounts**，以便包含应用程序池的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 服务帐户。<br /><br /> 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装路径下，创建 MDSTempDir 文件夹并为 **MDS_ServiceAccounts**分配权限。 此文件夹是为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序编译的临时编译文件所在的位置。<br /><br /> 在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]Web.config 文件中，配置`tempDirectory`的属性 **\<编译 >** 元素替换为 MDSTempDir 文件夹的路径。<br /><br /> <br /><br /> 如果您在编写安装进程的脚本，则可以打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 来注册 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 管理单元，但是必须手动执行其他步骤来完成配置。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 为您提供向导驱动的配置过程。 没有用于配置 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 的命令行过程。|[文件夹和文件权限 (Master Data Services)](../folder-and-file-permissions-master-data-services.md)<br /><br /> [Web 配置参考 (Master Data Services)](../web-configuration-reference-master-data-services.md)|  
|创建 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 为您的主数据创建 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库。|[创建 Master Data Services 数据库](create-a-master-data-services-database.md)|  
|创建 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 创建和配置 Web 应用程序以承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|[创建主数据管理器 Web 应用程序 (Master Data Services)](create-a-master-data-manager-web-application-master-data-services.md)|  
|将 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库与 Web 应用程序关联|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 将 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序与您的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库关联。|[将 Master Data Services 数据库与 Web 应用程序关联](associate-a-master-data-services-database-and-web-application.md)|  
|配置 Internet Explorer 增强安全性|在 Windows Server 2008 或 Windows Server 2008 R2 计算机上安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 时，可能必须配置 Internet Explorer 增强安全性以允许为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 应用程序站点编写脚本。 否则，浏览到服务器计算机上的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 应用程序站点将失败。|[Internet Explorer:增强的安全配置](https://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|将使用主数据的用户可以安装 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]。|[https://go.microsoft.com/fwlink/?LinkId=219530](https://go.microsoft.com/fwlink/?LinkId=219530)|  
|启用 Data Quality Services (DQS) 集成|对于 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]的用户，启用与 DQS 功能的集成，可用于匹配相似数据。|[实现 Data Quality Services 与 Master Data Services 的集成](enable-data-quality-services-integration-with-master-data-services.md)|  
|部署示例模型|示例模型包与 Master Data Services 一起安装，可以使用 MDSModelDeploy.exe 进行部署。|[在 SQL Server 中部署 MDS 示例](https://go.microsoft.com/fwlink/?LinkId=251486&clcid=0x409)|  
  
 如果您在安装过程中或初始配置过程中遇到问题，请参阅 TechNet Wiki 上的 [解决安装和配置问题](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) 。  
  
 如果不再需要计算机上的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，可以卸载 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 并确定是否删除不受卸载过程影响的项。 有关详细信息，请参阅 [卸载和删除 Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  
