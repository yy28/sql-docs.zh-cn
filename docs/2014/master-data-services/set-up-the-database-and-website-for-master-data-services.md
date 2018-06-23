---
title: 为 Master Data Services 数据库和网站设置 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 09e3e92d20182be2feb1c357cc1d3f518c55e5ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125629"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>为 Master Data Services 设置数据库和网站
  使用[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]若要设置数据库和网站[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)](MDS)  
  
 若要设置数据和网站，请完成以下任务。  
  
1.  创建数据库使用**数据库配置**页面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。  
  
     有关信息，请参阅[数据库配置页&#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)和[创建数据库向导&#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  创建新网站，选择默认网站，或选择另一个现有网站，使用**Web 配置**页面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。 然后将 MDS 数据库与你选择或创建的 Web 应用程序相关联。  
  
     有关信息，请参阅[网页配置&#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)和[创建网站对话框&#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  （可选）启用与 Data Quality Services 使用的集成**Web 配置**页面[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。  
  
     有关详细信息，请参阅[网页配置&#40;Master Data Services 配置管理器&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)和[Enable 数据质量 Services Integration with Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md)。  
  
 你还可以使用[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]指定 web 应用程序和服务与 MDS 数据库关联的设置。 例如，你可以指定加载数据的频率或发送验证电子邮件的频率。 有关详细信息，请参阅[系统设置 (Master Data Services)](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [Master Data Services 数据库](../../2014/master-data-services/master-data-services-database.md)   
 [主数据管理器 Web 应用程序](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  