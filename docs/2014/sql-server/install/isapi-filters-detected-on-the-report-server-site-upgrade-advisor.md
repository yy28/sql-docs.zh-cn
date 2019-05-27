---
title: 在报表服务器站点 （升级顾问） 上检测到 ISAPI 筛选器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 812fc3584f0d0742ea6065e4600da1f9a7755385
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094157"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>在报表服务器站点上检测到 ISAPI 筛选器（升级顾问）
  升级顾问检测到承载报表服务器和报表管理器虚拟目录的网站上存在一个或多个 ISAPI 筛选器。 中不支持 ISAPI 筛选器[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级之前，请验证 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序是否使用了网站上的 ISAPI 筛选器。 如果不需要 ISAPI 筛选器，您可以升级报表服务器。 安装程序将创建默认 URL，并且不为在 IIS 中运行的 ISAPI 筛选器提供支持。 如果需要 ISAPI 筛选器，则在找到承载 ISAPI 筛选器的其他方法（例如，使用 ISA Server 或继续在 IIS 中承载 ISAPI 筛选器）之前请不要进行升级。 在某些情况下，报表服务器支持 ASP.NET HTTPModules 作为 ISAPI 筛选器的替代项。 有关详细信息，请参阅 MSDN 上的 ASP.NET 文档。  
  
## <a name="corrective-action"></a>纠正措施  
 评估并使用其他解决方案来承载部署所需的 ISAPI 筛选器。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
