---
title: “创建 Web 应用程序”对话框（Master Data Services 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e9efc369885d183af3ceda0838ec2f814df8252a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>“创建 Web 应用程序”对话框（Master Data Services 配置管理器）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  使用“创建 Web 应用程序”  对话框可以创建 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序。 此 Web 应用程序在“Web 配置”  页上选择的网站中创建。  
  
## <a name="web-application"></a>Web 应用程序  
 Web 服务器从文件系统中的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** 文件夹为此 Web 应用程序提供内容。 此位置在安装过程中指定，路径默认为驱动器:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication。  
  
|控件名称|Description|  
|------------------|-----------------|  
|虚拟路径|选择要在其下创建 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的虚拟路径。 虚拟路径是用来访问 Web 应用程序的 URL 的一部分。<br /><br /> 对此列表进行筛选以便只显示可在其下创建 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的应用程序虚拟路径。 不能在其他 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序下创建 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序。|  
|别名|为 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序键入名称，或使用默认名称。 在 URL 中使用该名称从 Web 浏览器访问 Web 应用程序。|  
  
## <a name="application-pool"></a>应用程序池  
  
|控件名称|Description|  
|------------------|-----------------|  
|**名称**|为新的应用程序池键入唯一的友好名称，或者使用默认名称。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序将添加到这个应用程序池。<br /><br /> 应用程序池提供的边界可防止一个应用程序池中的应用程序影响另一个应用程序池中的应用程序。|  
|**User name**|键入来自 Active Directory 的域名和用户名。 此帐户是 Web 应用程序运行所在的应用程序池的标识。 此帐户应该与创建 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库时指定为服务帐户的帐户相同。<br /><br /> 此帐户添加到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中的 mds_exec 数据库角色，以便访问数据库。 有关详细信息，请参阅[数据库登录、用户和角色 (Master Data Services)](../master-data-services/database-logins-users-and-roles-master-data-services.md)。 它还会被添加到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows 组 **MDS_ServiceAccounts**，该组有权访问文件系统中的临时编译目录 **MDSTempDir**。 有关详细信息，请参阅[文件夹和文件权限 (Master Data Services)](../master-data-services/folder-and-file-permissions-master-data-services.md)。|  
|**密码**|键入指定用户帐户的密码。|  
|**确认密码**|重新键入指定用户帐户的密码。 **“密码”** 字段和 **“确认密码”** 字段必须包含相同的密码。|  
  
## <a name="see-also"></a>另请参阅  
 [“Web 配置”页（Master Data Services 配置管理器）](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)[Web 应用程序要求 &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [创建主数据管理器 Web 应用程序 &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
