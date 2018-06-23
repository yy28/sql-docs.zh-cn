---
title: 对 PowerPivot for SharePoint 安装进行故障排除 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: b4881ce3be8ede7d97dc2b71fb464b94b8677ca0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028709"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>排除 PowerPivot for SharePoint 安装故障
  如果看到错误而不是预期的页面和功能，请执行以下操作。  
  
-   查阅 SharePoint 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的发行说明以获取已知安装问题的解决办法。 发行说明随安装介质提供或在您下载软件的 Microsoft 网站上提供。  
  
    -   [SQL Server 2014 发行说明](http://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx)。  
  
-   请参阅 Technet wiki 主题[故障排除的 PowerPivot 的安装 （和其他外接）](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)。  
  
## <a name="issues"></a>问题  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>PowerPivot 库缩略图图形显示为红 X  
 一个可能原因是**PowerPivot 功能 Integration for Site Collections**处于非活动状态。 请完成以下操作：  
  
1.  在 PowerPivot 库库中，单击**站点设置**从齿轮图标![SharePoint 设置](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")或**主页**列表。  
  
2.  在 **“网站集管理”** 部分，单击 **“网站集功能”**。  
  
3.  单击 **“网站集功能”**。  
  
4.  验证**PowerPivot 功能 Integration for Site Collections**是**Active**。  
  
 有关此问题的其他原因，请参见[PowerPivot 库显示红色 X 图标](http://support.microsoft.com/kb/2361559)(http://support.microsoft.com/kb/2361559)。  
  
  