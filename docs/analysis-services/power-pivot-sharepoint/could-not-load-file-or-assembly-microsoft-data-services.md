---
title: "无法加载文件或程序集 Microsoft Data Services |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0daa7111e93a81c367fda433cc7b530a4c90e8f4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>无法加载文件或程序集 Microsoft 数据服务
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]具有 SharePoint 2010 环境中[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]for SharePoint，，如果你尝试执行数据馈送导出并且系统缺少 Microsoft ADO.NET Data Services 所需的版本将出现此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|找不到 ADO.NET Data Services 3.5 SP1。|  
|消息正文|无法加载文件或程序集“Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089”或其依赖项之一。 系统找不到指定的文件。|  
  
## <a name="explanation"></a>解释  
 SharePoint 2010 包括“作为数据馈送导出”按钮，您可以使用该按钮将 SharePoint 列表作为 XML 数据馈送导出。 此外，SharePoint 模式下的 Reporting Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 都支持要求 ADO.NET Data Services 的数据馈送功能。  
  
 如果 ADO.NET Data Services 未安装，则在您请求数据馈送时，将发生此错误。  
  
## <a name="user-action"></a>用户操作  
  
1.  转到针对 SharePoint 2010 的硬件和软件要求文档 [确定硬件和软件要求 (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734)。  
  
2.  在 **“安装必备软件”**中，找到用于与您正在使用的操作系统相对应的 ADO.NET Data Services 3.5 的链接。  
  
3.  单击该链接并且运行安装该服务的安装程序。  
  
## <a name="see-also"></a>另请参阅  
 [将 Power Pivot 解决方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
