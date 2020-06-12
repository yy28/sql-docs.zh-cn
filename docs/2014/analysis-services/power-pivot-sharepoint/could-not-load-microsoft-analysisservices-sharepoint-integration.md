---
title: 无法加载文件或程序集 &#39;3.5.0.0，Version =，Culture = 中立，PublicKeyToken = b77a5c561934e089&#39; 或其依赖项之一。 系统找不到指定的文件。 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9bcfdde8b3536bbbf8b2429d51a9ee9aecf0d437
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547499"
---
# <a name="could-not-load-file-or-assembly-39microsoftdataservices-version3500-cultureneutral-publickeytokenb77a5c561934e08939-or-one-of-its-dependencies-the-system-cannot-find-the-file-specified"></a>无法加载文件或程序集 &#39;3.5.0.0，Version =，Culture = 中立，PublicKeyToken = b77a5c561934e089&#39; 或其依赖项之一。 系统找不到指定的文件。
  在具有 PowerPivot for SharePoint 的 SharePoint 2010 环境中，如果您尝试执行数据馈送导出并且系统缺少 Microsoft ADO.NET Data Services 的必需版本，则会出现此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|PowerPivot for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|找不到 ADO.NET Data Services 3.5 SP1。|  
|消息正文|无法加载文件或程序集“Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089”或其依赖项之一。 系统找不到指定的文件。|  
  
## <a name="explanation"></a>说明  
 SharePoint 2010 包括“作为数据馈送导出”按钮，您可以使用该按钮将 SharePoint 列表作为 XML 数据馈送导出。 此外，SharePoint 模式下的 Reporting Services 和 PowerPivot for SharePoint 都支持要求 ADO.NET Data Services 的数据馈送功能。  
  
 如果 ADO.NET Data Services 未安装，则在您请求数据馈送时，将发生此错误。  
  
## <a name="user-action"></a>用户操作  
  
1.  请参阅 SharePoint 2010 的硬件和软件要求文档，[确定硬件和软件要求（sharepoint 2010）](https://go.microsoft.com/fwlink/?LinkId=169734) （ https://go.microsoft.com/fwlink/?LinkId=169734) 。  
  
2.  在 "**安装必备软件**" 中，找到与所使用的操作系统相对应的 ADO.NET Data Services 3.5 的链接。  
  
3.  单击该链接并且运行安装该服务的安装程序。  
  
## <a name="see-also"></a>另请参阅  
 [将 PowerPivot 解决方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
