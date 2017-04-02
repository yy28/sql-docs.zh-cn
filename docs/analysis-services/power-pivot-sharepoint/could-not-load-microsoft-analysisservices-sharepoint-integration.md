---
title: "无法加载文件或程序集“Microsoft.AnalysisServices.SharePoint.Integration” | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 7
---
# 无法加载文件或程序集“Microsoft.AnalysisServices.SharePoint.Integration”
  在具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 2010 环境中，如果用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的应用程序级别的解决方案未正确部署，将发生此错误。  
  
## 详细信息  
  
|||  
|-|-|  
|适用于|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Powerpivotwebapp 解决方案未部署或者未正确部署。|  
|消息正文|无法加载文件或程序集“Microsoft.AnalysisServices.SharePoint.Integration”|  
  
## 解释  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用解决方案包在 SharePoint 服务器上部署其功能。 解决方案之一未正确部署。 因此，只要你尝试在 SharePoint 站点上打开 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库或者其他 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 应用程序页，就会出现此错误。  
  
## 用户操作  
 部署解决方案包。  
  
1.  在管理中心的“系统设置”中，单击 **“管理场解决方案”**。  
  
2.  单击 **“Powerpivotwebapp”**。  
  
3.  单击 **“部署解决方案”**。  
  
4.  选择发生了此错误的 Web 应用程序。 如果存在多个 Web 应用程序，则为所有这些应用程序都重新部署解决方案。  
  
5.  单击 **“确定”**。  
  
## 另请参阅  
 [将 Power Pivot 解决方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  