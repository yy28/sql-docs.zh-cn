---
title: "Power Pivot for SharePoint 安装疑难解答 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Power Pivot for SharePoint 安装疑难解答
  如果看到错误而不是预期的页面和功能，请执行以下操作。  
  
-   查阅 SharePoint 和 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的发行说明以获取已知安装问题的解决办法。 发行说明随安装介质提供或在您下载软件的 Microsoft 网站上提供。  
  
    -   [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)  
  
-   请参阅 TechNet wiki 主题：[PowerPivot（和其他外接程序）安装疑难解答](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)。  
  
## 问题  
  
### Power Pivot 库缩略图图形显示为红色 X  
 一个可能的原因是，“针对网站集的 **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 功能集成”** 未处于活动状态。 请完成以下操作：  
  
1.  在 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] Gallery 库中，从齿轮图标 ![SharePoint 设置](../analysis-services/media/as-sharepoint2013-settings-gear.png "SharePoint 设置") 或“主页”列表单击“网站设置”。  
  
2.  在 **“网站集管理”** 部分，单击 **“网站集功能”**。  
  
3.  单击 **“网站集功能”**。  
  
4.  确认“针对网站集的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 功能集成”为“活动”状态。  
  
 有关此问题的其他原因，请参阅 [PowerPivot Gallery 对图标显示红色 X](http://support.microsoft.com/kb/2361559) (http://support.microsoft.com/kb/2361559)。  
  
  