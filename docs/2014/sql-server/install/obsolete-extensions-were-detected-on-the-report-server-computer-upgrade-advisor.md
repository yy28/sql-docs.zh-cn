---
title: 报表服务器计算机 （升级顾问） 上检测到过时的扩展插件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93a971b82fa4bafd1d8fb51a148b7e488c7d6d20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093804"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>在报表服务器计算机上检测到过时的扩展插件（升级顾问）
  升级顾问检测到当前版本中不再可用的一个或多个呈现扩展插件。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>描述  
 报表服务器配置为使用在此版本中不再支持的一个或多个扩展插件。 不再支持的扩展插件包括：  
  
-   HTML OWC 呈现扩展插件  
  
-   HTML 3.2 呈现扩展插件  
  
 升级可以继续，但是不支持的功能将不再可用于升级后的报表服务器。  
  
 直到您要求这些扩展插件，则在找到针对这些要求的替代解决方案前，不要升级。 您可能需要获取或生成一个提供相同或类似功能的自定义呈现扩展插件。  
  
## <a name="corrective-action"></a>纠正措施  
 评估 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中包含的当前功能集以确定支持的功能是否满足您的要求。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
