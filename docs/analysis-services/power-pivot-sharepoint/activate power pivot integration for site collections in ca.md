---
title: "在管理中心中针对网站集激活 Power Pivot 功能集成 | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 在管理中心中针对网站集激活 Power Pivot 功能集成
  如果你使用了“现有场”安装选项来安装 SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则需要为特定的网站集激活 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能集成。 如果你使用“新服务器”选项安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则可以跳过此任务，因为 SQL Server 安装程序在配置你的部署时已经为根网站集激活了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能集成。  
  
 网站集级别的功能激活是使应用程序页和模板对你的站点可用所必需的，包括用于计划的数据刷新的配置页以及用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库和数据馈送库的应用程序页。  
  
 对于支持 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查询处理的每个网站集，你必须激活 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 集成。  
  
## 先决条件  
 您必须是网站集管理员。  
  
## 激活 Power Pivot 功能  
  
1.  在 SharePoint 站点上，单击 **“网站操作”**。  
  
     默认情况下，通过端口 80 访问 SharePoint Web 应用程序。 这意味着你通常可以通过输入 http://\<computer name> 来打开根网站集，从而访问 SharePoint 网站。  
  
2.  单击 **“网站设置”**。  
  
3.  在“网站集管理”中，单击 **“网站集功能”**。  
  
4.  向下滚动该页，直到找到“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 集成网站集功能”。  
  
5.  单击 **“激活”**。  
  
6.  通过打开各站点并单击 **“网站操作”**，对于其他网站集重复上述操作。  
  
## 另请参阅  
 [在管理中心中管理和配置 Power Pivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [初始安装 (Power Pivot for SharePoint)](http://msdn.microsoft.com/zh-cn/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [Power Pivot for SharePoint 2010 安装](http://msdn.microsoft.com/zh-cn/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  