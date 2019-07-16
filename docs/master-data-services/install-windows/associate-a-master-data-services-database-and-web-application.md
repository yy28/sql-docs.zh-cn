---
title: 将 Master Data Services 数据库与 Web 应用程序关联 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 78dda3464aab255834acffd16afd298021c40fd5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945024"
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>将 Master Data Services 数据库与 Web 应用程序关联

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  将您的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序与 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库关联以指定要用于 Web 操作的数据库。  
  
## <a name="prerequisites"></a>系统必备  
  
-   [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 必须安装在本地计算机上。 有关详细信息，请参阅 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)。  
  
-   本地 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序必须存在。 有关详细信息，请参阅[创建主数据管理器 Web 应用程序 (Master Data Services)](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)。  
  
-   本地或远程 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库必须存在。 有关详细信息，请参阅 [创建 Master Data Services 数据库](../../master-data-services/install-windows/create-a-master-data-services-database.md)。  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>将 Master Data Services 数据库与 Web 应用程序关联  
  
1.  打开 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]。  
  
2.  在左窗格中单击 **“Web 配置”** 。  
  
3.  在 **“Web 配置”** 页的 **“Web 应用程序”** 下，从 **“网站”** 列表中选择包含 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序的网站。  
  
4.  在 **“Web 应用程序”** 框中，选择承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]的 Web 应用程序。  
  
5.  在 **“将应用程序与数据库相关联”** 下，单击 **“选择”** 。 将打开 **“连接到数据库”** 对话框。  
  
6.  指定承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 实例的连接信息，然后单击 **“连接”** 。  
  
7.  从 **“Master Data Services 数据库”** 列表选择要与 Web 应用程序关联的数据库，然后单击 **“确定”** 。  
  
8.  在 **“将应用程序与数据库相关联”** 下，验证实例和数据库信息是正确的，然后单击 **“应用”** 。  
  
## <a name="next-steps"></a>后续步骤  
  
-   在创建 Web 应用程序时，将自动启用对 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web 服务的编程访问。 为使开发人员访问服务元数据以便轻松地为编程访问生成代理类，启用元数据发布。 有关详细信息，请参阅 [创建主数据管理器 Web 服务代理类](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)。  
  
-   将用户和组添加到 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。 如果没有向任何用户或组授予访问 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]的权限，您必须使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 系统管理员凭据打开 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 。 有关详细信息，请参阅[管理员 (Master Data Services)](../../master-data-services/administrators-master-data-services.md) 和[用户和组 (Master Data Services)](../../master-data-services/users-and-groups-master-data-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
 [“Web 配置”页（Master Data Services 配置管理器）](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
