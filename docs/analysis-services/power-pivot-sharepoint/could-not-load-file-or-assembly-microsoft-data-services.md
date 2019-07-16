---
title: 无法加载文件或程序集 Microsoft 数据服务 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9472fffb790d8d18ced8d2a528011927717aabc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164156"
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>无法加载文件或程序集 Microsoft 数据服务
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 2010 环境中，如果你尝试执行数据馈送导出并且系统缺少 Microsoft ADO.NET Data Services 的必需版本，则会出现此错误。  
  
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
  
1.  转到针对 SharePoint 2010 的硬件和软件要求文档[确定硬件和软件要求 (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734) 。  
  
2.  在 **“安装必备软件”** 中，找到用于与您正在使用的操作系统相对应的 ADO.NET Data Services 3.5 的链接。  
  
3.  单击该链接并且运行安装该服务的安装程序。  
  
## <a name="see-also"></a>请参阅  
 [将 Power Pivot 解决方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
