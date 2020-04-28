---
title: 直接浏览到报表服务器（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6945828b2eba829c32d717c13393c9fbda4fc43e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952214"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>直接浏览到报表服务器（升级顾问）
  升级顾问检测到您的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]当前安装正在直接浏览到 Report Server 虚拟目录。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 升级顾问检测到您的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]当前安装正在直接浏览到 Report Server 虚拟目录，例如**http://\<server name>/reportserver**。 在当前版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中不支持它。  
  
> [!NOTE]  
>  此规则是一则警告，将不阻止升级。  
  
## <a name="corrective-action"></a>纠正措施  
 浏览使用用于文档库的 SharePoint 用户界面，或**使用\<http://server name>/sharepoint site>/_vti_bin/reportserver**。  
  
  
