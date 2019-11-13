---
title: 排查 PowerPivot for SharePoint 安装问题 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f70af740fb3fe8310a5306368c1bf48c6f357419
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952002"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>排除 PowerPivot for SharePoint 安装故障
  如果看到错误而不是预期的页面和功能，请执行以下操作。  
  
-   查阅 SharePoint 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的发行说明以获取已知安装问题的解决办法。 发行说明随安装介质提供或在您下载软件的 Microsoft 网站上提供。  
  
    -   [SQL Server 2014 发行说明](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx)。  
  
-   请参阅 Technet wiki 主题： [PowerPivot （和其他外接程序）安装疑难解答](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)。  
  
## <a name="issues"></a>问题  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>PowerPivot 库缩略图图形显示为红 X  
 一个可能的原因是 "**网站集的 PowerPivot 功能集成**" 未处于活动状态。 请完成以下操作：  
  
1.  在 PowerPivot 库中，从齿轮图标![Sharepoint 设置](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Sharepoint")设置或**Home**列表中单击 "**网站设置**"。  
  
2.  在 **“网站集管理”** 部分，单击 **“网站集功能”** 。  
  
3.  单击 **“网站集功能”** 。  
  
4.  验证 "**网站集的 PowerPivot 功能集成**" 处于**活动状态**。  
  
 有关此问题的其他原因，请参阅[PowerPivot 库显示图标的红色 X](https://support.microsoft.com/kb/2361559) （ https://support.microsoft.com/kb/2361559)。  
  
  
