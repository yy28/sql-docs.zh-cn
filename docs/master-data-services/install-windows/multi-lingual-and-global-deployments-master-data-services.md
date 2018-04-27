---
title: 多语言和全球部署 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d5694035db52205d17a482a5ac8b8a79144d163
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>多语言和全球部署 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的所有语言的组件和工具部署。 有关详细信息，请参阅 [Local Language Versions in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md)。  
  
## <a name="how-languages-are-used"></a>如何使用语言  
 下表说明了对 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 组件和工具的语言支持情况。  
  
|组件或工具|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装程序|当希望以不同于安装程序语言的语言来提供和支持 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序时，请选择“英语”安装程序。 有关详细信息，请参阅下面的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 说明。|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|安装程序语言决定 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 语言。 例如，如果为安装程序语言选择了“德语”，则在该计算机上提供德语形式的 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] 。|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|当运行英语形式的安装程序时，将以所有应用程序语言提供和支持 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 可以用其中的任何一种应用程序语言来显示，而且会根据客户端 Web 浏览器的语言首选项来接受特定于区域设置的输入。 如果为不支持的应用程序语言配置语言首选项， [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 将默认使用“英语”。<br /><br /> 运行非英文版的安装程序时，将包括所有其他应用程序语言的资源，但是如果客户端使用的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 语言不同于所选的安装程序语言，则不支持上述情形。 如果尝试访问不同于安装程序语言的 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 语言版本，可能会在应用程序中遇到数据显示和输入问题。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 数据库中的信息不是任何区域设置专用的。 这使得 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 可以决定如何显示日期和数字等信息，其格式由客户端 Web 浏览器的语言首选项决定。|  
  
## <a name="see-also"></a>另请参阅  
 [安装 Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
