---
title: 直接浏览到报表服务器 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 870937f4dffe356ca2216335c74566efc73d2a52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095540"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>直接浏览到报表服务器（升级顾问）
  升级顾问检测到您当前安装的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]正在直接浏览到报表服务器虚拟目录。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级顾问检测到您当前安装的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]正在直接浏览到报表服务器虚拟目录，例如**http://\<服务器名称 > / ReportServer**。 在当前版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中不支持它。  
  
> [!NOTE]  
>  此规则是一则警告，将不阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 浏览文档库中使用 SharePoint 用户界面或使用**http://\<服务器名称 > / sharepoint 站点 >/_vti_bin/reportserver**。  
  
  
