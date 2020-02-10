---
title: 为 Master Data Services 设置数据库和网站 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 478dea9095fe22a437aecf138c22374b5a70885b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054096"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>为 Master Data Services 设置数据库和网站
  使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 为 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 设置数据库和网站  
  
 若要设置数据和网站，请完成以下任务。  
  
1.  使用中[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]的 "**数据库配置**" 页创建数据库。  
  
     有关信息，请参阅[数据库配置页 &#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)和[创建数据库向导 &#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md)。  
  
2.  创建新网站，选择默认网站，或者使用中[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]的 " **Web 配置**" 页选择另一个现有网站。 然后将 MDS 数据库与你选择或创建的 Web 应用程序相关联。  
  
     有关信息，请参阅[Web 配置页 &#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)和 "[创建网站" 对话框 &#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md)。  
  
3.  可有可无使用中[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]的 " **Web 配置**" 页启用与 Data Quality Services 的集成。  
  
     有关详细信息，请参阅[Web 配置页 &#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)和[启用 Data Quality Services 与 Master Data Services 集成](install-windows/enable-data-quality-services-integration-with-master-data-services.md)。  
  
 你还可以使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 指定与 MDS 数据库相关联的 Web 应用程序和服务的设置。 例如，你可以指定加载数据的频率或发送验证电子邮件的频率。 有关详细信息，请参阅[系统设置 (Master Data Services)](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Master Data Services 数据库](../../2014/master-data-services/master-data-services-database.md)   
 [主数据管理器 Web 应用程序](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
