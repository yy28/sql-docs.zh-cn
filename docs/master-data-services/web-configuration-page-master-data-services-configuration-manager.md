---
title: Web 配置页（Master Data Services 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9d685a3f143e97aad040b51fa18b4d66ce701072
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400369"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>“Web 配置”页（Master Data Services 配置管理器）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  使用“Web 配置”  页配置网站和 Web 应用程序。 也可启用 Data Quality Services。  
  
## <a name="configure-the-web-application"></a>配置 Web 应用程序  
  
|控件名称|描述|  
|------------------|-----------------|  
|**网站**|创建新网站，选择默认网站，或者选择其他可用的网站（如果列出）。 此列表显示在本地计算机上的 Internet Information Services (IIS) 中定义的网站。 创建新网站时，将自动创建新的 Web 应用程序。 选择默认网站或其他现有的网站时，必须手动创建应用程序。|  
|**Web 应用程序**|选择用于配置的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序。 此框仅显示所选网站中的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序。<br /><br /> 如果什么都没显示，请单击“创建”以创建网站。|  
|**创建**|打开 **“创建 Web 应用程序”** 对话框，从中可以在所选网站中创建 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序。 仅当选定的网站没有配置为 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的根 Web 应用程序时，此按钮才会启用。|  
  
## <a name="associate-application-with-database"></a>将应用程序与数据库相关联  
  
|控件名称|描述|  
|------------------|-----------------|  
|**选择**|打开 **“连接到服务器”** 对话框，从中连接到某一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例并选择要与所选 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 应用程序相关联的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 数据库。|  
|**SQL Server 实例**|显示承载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的所选 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例的名称。 在您连接到某一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例并选择某一数据库之前，此项为空。|  
|**“数据库”**|显示与所选 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 应用程序相关联的 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 数据库的名称。 在您连接到某一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例并选择某一数据库之前，此项为空。|  
  
## <a name="enable-dqs-integration"></a>启用 DQS 集成  
  
|控件名称|描述|  
|------------------|-----------------|  
|**启用与 Data Quality Services 的集成**|选择此选项可启用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]中提供的数据质量功能。 有关详细信息，请参阅 [实现 Data Quality Services 与 Master Data Services 的集成](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)。|  
  
## <a name="see-also"></a>另请参阅  
[Master Data Services 的安装和配置](../master-data-services/master-data-services-installation-and-configuration.md)[Web 应用程序要求 &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [创建主数据管理器 Web 应用程序 &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
