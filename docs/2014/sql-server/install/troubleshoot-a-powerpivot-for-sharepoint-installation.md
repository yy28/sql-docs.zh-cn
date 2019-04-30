---
title: 对 PowerPivot for SharePoint 安装进行故障排除 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 471bfe1a93e76630e6699a2ff07fcf5c6bddc913
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267892"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>排除 PowerPivot for SharePoint 安装故障
  如果看到错误而不是预期的页面和功能，请执行以下操作。  
  
-   查阅 SharePoint 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的发行说明以获取已知安装问题的解决办法。 发行说明随安装介质提供或在您下载软件的 Microsoft 网站上提供。  
  
    -   [SQL Server 2014 发行说明](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx)。  
  
-   请参阅 Technet wiki 主题[故障排除安装 PowerPivot （和其他加载项）](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)。  
  
## <a name="issues"></a>问题  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>PowerPivot 库缩略图图形显示为红 X  
 一个可能的原因是**PowerPivot 功能集成网站集**未处于活动状态。 请完成以下操作：  
  
1.  在 PowerPivot Gallery 库中，单击**站点设置**从齿轮图标![SharePoint 设置](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")或**主页**列表。  
  
2.  在 **“网站集管理”** 部分，单击 **“网站集功能”**。  
  
3.  单击 **“网站集功能”**。  
  
4.  验证是否**PowerPivot 功能集成的站点集合**是**Active**。  
  
 有关此问题的其他原因，请参阅[PowerPivot 库将显示红色 X 图标](https://support.microsoft.com/kb/2361559)(https://support.microsoft.com/kb/2361559)。  
  
  
