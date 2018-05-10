---
title: 激活 Power Pivot Integration for Site Collections in CA |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 976ad94b2c58d86a1b7731bfd3a9aa74097f3b29
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>激活 Power Pivot Integration for Site Collections in CA
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果你使用了“现有场”安装选项来安装 SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则需要为特定的网站集激活 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能集成。 如果你使用“新服务器”选项安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则可以跳过此任务，因为 SQL Server 安装程序在配置你的部署时已经为根网站集激活了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能集成。  
  
 网站集级别的功能激活是使应用程序页和模板对你的站点可用所必需的，包括用于计划的数据刷新的配置页以及用于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 库和数据馈送库的应用程序页。  
  
 对于支持 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查询处理的每个网站集，你必须激活 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 集成。  
  
## <a name="prerequisites"></a>必要條件  
 您必须是网站集管理员。  
  
## <a name="activate-power-pivot-features"></a>激活 Power Pivot 功能  
  
1.  在 SharePoint 站点上，单击 **“网站操作”**。  
  
     默认情况下，通过端口 80 访问 SharePoint Web 应用程序。 这意味着，通常可以通过输入 http:// 访问 SharePoint 站点\<计算机名称 > 若要打开根网站集。  
  
2.  单击 **“网站设置”**。  
  
3.  在“网站集管理”中，单击 **“网站集功能”**。  
  
4.  向下滚动该页，直到找到“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 集成网站集功能”。  
  
5.  单击 **“激活”**。  
  
6.  通过打开各站点并单击 **“网站操作”**，对于其他网站集重复上述操作。  
  
## <a name="see-also"></a>另请参阅  
 [在管理中心中管理和配置 Power Pivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [初始配置 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [Power Pivot for SharePoint 2010 安装](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
