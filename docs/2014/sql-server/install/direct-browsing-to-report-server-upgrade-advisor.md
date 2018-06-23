---
title: 直接浏览报表服务器 （升级顾问） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f08bc5d25eed160b814bfcdc255e1f198836da2b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014939"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>直接浏览到报表服务器（升级顾问）
  升级顾问检测到你当前安装的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]直接浏览到报表服务器虚拟目录。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 升级顾问检测到你当前安装的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]直接浏览到报表服务器虚拟目录，例如**http://\<服务器名称 > / ReportServer**。 在当前版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中不支持它。  
  
> [!NOTE]  
>  此规则是一则警告，将不阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 浏览使用用于文档库的 SharePoint 用户界面或使用**http://\<服务器名称 > / sharepoint 站点 >/_vti_bin/reportserver**。  
  
  