---
title: "Master Data Services 的安装任务 | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bb7aa3e7-8807-42c8-884f-0e41d7a20837
caps.latest.revision: 32
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: ffeb77252907d7b2dfae4c60491ee6d9b239e641
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="installation-tasks-for-master-data-services"></a>Master Data Services 的安装任务
  本文概述了安装任务，随附说明链接。 有关安装和配置 Master Data Services 的演练，请参阅 [Master Data Services 的安装和配置](../../master-data-services/master-data-services-installation-and-configuration.md) 
  
-   [安装前任务](#preinstall)：在安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]前验证系统要求。  
  
-   [安装操作](#install)：通过使用 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装程序或命令提示符安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [安装后任务](#postinstall)：打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 以便完成安装后操作。 创建和配置 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序和 Web 服务并部署示例模型。  
  
##  <a name="preinstall"></a> 安装前任务  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|验证安装要求|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的计算机必须满足以下方面的最低要求：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序。<br /><br /> [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序和 Web 服务。<br /><br /> [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库（如果数据库所在的计算机与 Web 应用程序所在的计算机相同）。<br /><br /> <br /><br /> 通过只在 Web 服务器计算机上运行安装程序并在运行支持的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 版本的远程计算机上创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，可以单独安装 Web 服务器计算机和数据库服务器计算机。|[SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)<br /><br /> [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)<br /><br /> [Web 应用程序要求 (Master Data Services)](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)<br /><br /> [数据库要求 (Master Data Services)](../../master-data-services/install-windows/database-requirements-master-data-services.md)|  
|配置所需的角色、角色服务和功能|运行安装程序前，请使用所需的 Windows 角色、角色服务和功能配置计算机。<br /><br /> 注意：尽管你可以在工作流的后面部分执行此步骤，但是在运行安装程序前进行配置很有用，因为这样你可以执行紧挨安装后面的 Web 配置任务。|[Web 应用程序要求 (Master Data Services)](../../master-data-services/install-windows/web-application-requirements-master-data-services.md)|  
|查看语言支持注意事项|确定要安装和运行 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 所用的语言。|[多语言和全球部署 (Master Data Services)](../../master-data-services/install-windows/multi-lingual-and-global-deployments-master-data-services.md)|  
  
##  <a name="install"></a> 安装操作  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序|在将承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序和 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服务的计算机上，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序或命令提示符安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序时， [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 将显示在 **“功能选择”** 页上的 **“共享功能”**下。 使用命令提示符时， [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 作为功能参数提供。 请注意，命令行安装过程将安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]，但不会对它进行配置。 您必须使用 Master Data Services 配置管理器对其进行配置。<br /><br /> 安装过程：<br /><br /> 在您为共享功能指定的位置安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 文件夹和文件，并为这些对象分配权限。<br /><br /> 在全局程序集缓存 (GAC) 中注册 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 程序集。<br /><br /> 安装 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。|[使用安装向导安装 SQL Server 2016（安装程序）](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)<br /><br /> [文件夹和文件权限 (Master Data Services)](../../master-data-services/folder-and-file-permissions-master-data-services.md)|  
  
##  <a name="postinstall"></a> 安装后任务  
  
|操作|详细信息|相关主题|  
|------------|-------------|--------------------|  
|打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 以便完成安装后操作|安装完成之后，打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 在本地计算机上执行以下安装后操作：<br /><br /> 创建一个 Windows 组 **MDS_ServiceAccounts**，以便包含应用程序池的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 服务帐户。<br /><br /> 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装路径下，创建 MDSTempDir 文件夹并为 **MDS_ServiceAccounts**分配权限。 此文件夹是为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序编译的临时编译文件所在的位置。<br /><br /> 在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.config 文件中，使用 MDSTempDir 文件夹的路径配置 \<> 元素的 tempDirectory 属性。|[文件夹和文件权限 (Master Data Services)](../../master-data-services/folder-and-file-permissions-master-data-services.md)<br /><br /> [Web 配置参考 (Master Data Services)](../../master-data-services/web-configuration-reference-master-data-services.md)|  
|创建 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 为您的主数据创建 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库。|[创建 Master Data Services 数据库](../../master-data-services/install-windows/create-a-master-data-services-database.md)|  
|创建 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 创建和配置 Web 应用程序以承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|[创建主数据管理器 Web 应用程序 (Master Data Services)](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)|  
|将 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库与 Web 应用程序关联|使用 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 将 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序与您的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库关联。|[将 Master Data Services 数据库与 Web 应用程序关联](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md)|  
|配置 Internet Explorer 增强安全性|在 Windows Server 2012 计算机上安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 时，可能必须配置 Internet Explorer 增强安全性以允许为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 应用程序站点编写脚本。 否则，浏览到服务器计算机上的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 应用程序站点将失败。|[Internet Explorer：增强安全性配置](http://go.microsoft.com/fwlink/p/?LinkId=223869)|  
|安装 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|将使用主数据的用户可以安装 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]。|[http://go.microsoft.com/fwlink/?LinkID=398159](http://go.microsoft.com/fwlink/?LinkID=398159)|  
|启用 Data Quality Services (DQS) 集成|对于 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]的用户，启用与 DQS 功能的集成，可用于匹配相似数据。|[实现 Data Quality Services 与 Master Data Services 的集成](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)|  
|部署示例模型|示例模型包与 Master Data Services 一起安装，可以使用 MDSModelDeploy.exe 进行部署。|[在 SQL Server 中部署 MDS 示例](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)|
  
 如果您在安装过程中或初始配置过程中遇到问题，请参阅 TechNet Wiki 上的 [解决安装和配置问题](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-installation-and-configuration-issues-master-data-services.aspx) 。  
  
 如果不再需要计算机上的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，可以卸载 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 并确定是否删除不受卸载过程影响的项。 有关详细信息，请参阅 [卸载和删除 Master Data Services](../../sql-server/install/uninstall-and-remove-master-data-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
  

