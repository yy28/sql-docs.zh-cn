---
title: 支持的 SharePoint 和 Reporting Services 服务器及外接程序 (SQL Server 2014) 的组合 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 49b19aaf7d34b052eac0e53c44814a961d6c4b74
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194790"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>支持的 SharePoint 和 Reporting Services 服务器及外接程序的组合 (SQL Server 2014)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器可在 SharePoint 模式下安装，并且可与 SharePoint 部署集成。 在报表服务器、SharePoint 的 Reporting Services 外接程序和 SharePoint 产品的所有组合中，并非所有功能都受支持。 本主题概述支持的组合。 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，集成是组合以下各项的结果：  
  
-   为 SharePoint 模式配置的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器的版本。  
  
-   SharePoint 产品。  
  
-   您在 SharePoint 服务器上安装的用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>支持的 SharePoint 与 Reporting Services 组件之间的组合  
 下表汇总了报表服务器、SharePoint 产品的 Reporting Services 外接程序和 SharePoint 产品之间支持的组合。 不支持下表中未列出的组合  
  
### <a name="supported-combinations"></a>支持的组合  
  
||报表服务器|外接程序|SharePoint 版本|是否支持|  
|-|-------------------|-------------|------------------------|---------------|  
|@shouldalert|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|是|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|是|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是<br /><br /> 例外：不支持 Power View 集成。|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|是|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|是|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|是|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|是|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|是|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|是|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|是|  
  
 有关详细信息[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]功能以及报表服务器模式，请参见[Reporting Services 报表服务器](../reporting-services-report-server.md)。  
  
 **其他说明：**  
  
-   支持 SharePoint 2013 （包括 Power View 集成）需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器以及 SQL Server 2012 SP1 或更高版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序版本。  
  
-   在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引入 Power View。 因此，Power View 与 SharePoint 2010 集成需要该外接程序的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更高版本。  
  
-   SQL Server 2012（或更高版本）报表服务器不支持 SQL Server 2008 R2 外接程序。 SharePoint 2010 必备组件安装程序会自动安装 SQL Server 2008 R2 外接程序。 必须在安装外接程序的更新版本前卸载它。 不支持外接程序的就地升级。  
  
-   **升级：** 装有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序的 SharePoint 2010 无法就地升级到 SharePoint 2013。 SharePoint 2013 需要 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 外接程序和报表服务器的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或更高版本。 有关升级的详细信息，请参阅[升级和迁移 Reporting Services](upgrade-and-migrate-reporting-services.md)。  
  
## <a name="see-also"></a>请参阅  
 [在哪里可以找到 Reporting Services 外接程序用于 SharePoint 产品](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [SQL Server 2014 的版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [升级和迁移 Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
