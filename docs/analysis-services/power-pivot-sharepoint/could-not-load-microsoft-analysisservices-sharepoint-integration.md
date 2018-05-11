---
title: 无法加载 Microsoft.AnalysisServices.SharePoint.Integration |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31f0b3c7dec264a9d1ee816eb591d2c0b2616961
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="could-not-load-microsoftanalysisservicessharepointintegration"></a>无法加载 Microsoft.AnalysisServices.SharePoint.Integration
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 2010 环境中，如果用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的应用程序级别的解决方案未正确部署，将发生此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Powerpivotwebapp 解决方案未部署或者未正确部署。|  
|消息正文|无法加载文件或程序集“Microsoft.AnalysisServices.SharePoint.Integration”|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用解决方案包在 SharePoint 服务器上部署其功能。 解决方案之一未正确部署。 因此，只要你尝试在 SharePoint 站点上打开 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库或者其他 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 应用程序页，就会出现此错误。  
  
## <a name="user-action"></a>使用者動作  
 部署解决方案包。  
  
1.  在管理中心的“系统设置”中，单击 **“管理场解决方案”**。  
  
2.  单击 **“Powerpivotwebapp”**。  
  
3.  单击 **“部署解决方案”**。  
  
4.  选择发生了此错误的 Web 应用程序。 如果存在多个 Web 应用程序，则为所有这些应用程序都重新部署解决方案。  
  
5.  单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [将 Power Pivot 解决方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
