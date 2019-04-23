---
title: SharePoint 集成与 2008年和 2008 R2 报表服务器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2d5a4394a9fbbf9ff7daa54ed7ba6a8b28921bd5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945303"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>SharePoint 与 2008 和 2008 R2 报表服务器集成
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 版本引入了一种体系结构，在此体系结构中，SharePoint 模式现在基于 SharePoint 共享服务。 在 SharePoint 管理中心中上完成新功能的管理**管理服务**并**管理器服务应用程序**页。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]以前为 SharePoint 集成的体系结构仍支持[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]用于 SharePoint 2010 产品，与以前版本的报表服务器集成 SharePoint 2010 外接程序。  
  
 您将用于管理旧体系结构的“SharePoint 管理中心”页在以下位置提供：  
  
1.  在 SharePoint 管理中心内单击**常规应用程序设置**。  
  
2.  该组**SQL Server Reporting Services （2008年和 2008 R2）** 包含的链接和较旧的体系结构的管理页面  
  
## <a name="server-integration-architecture"></a>服务器集成体系结构  
 将报表服务器与 SharePoint 产品的实例集成后，项和属性将存储在 SharePoint 内容数据库中。 这在影响内容存储、保护及访问方式的各种服务器技术之间提供了更深层次的集成。  
  
 将报表项和报表属性存储在 SharePoint 内容数据库中，您将可以执行以下操作：浏览 SharePoint 库中的报表服务器内容类型；使用相同的权限级别和身份验证提供程序（用于对位于 SharePoint 站点上的其他业务文档进行访问控制）来保护报表项；使用协作和文档管理功能签入和签出报表以供修改；使用警报查明是否已更改某个报表项；在应用程序的页面和站点中嵌入或自定义报表查看器 Web 部件。 如果您在 SharePoint 站点中有足够的权限，则还可以从共享数据源生成报表模型并使用报表生成器来创建报表。  
  
 报表服务器仍然提供所有数据处理、呈现及传递功能。 它还支持关于快照和报表历史记录的所有计划报表处理。 从 SharePoint 站点打开报表时，报表服务器端点将依次执行以下操作：连接到报表服务器、创建会话、准备处理该报表、检索数据、将该报表合并到报表布局中、在报表查看器 Web 部件中显示该报表。 在报表处于打开状态时，可以将报表导出为不同的应用程序格式，还可以通过深入到报表下层或一直单击到相关报表的方式实现数据交互。 导出和报表交互操作均在报表服务器上进行。  
  
 报表服务器与 SharePoint 进行操作和数据的同步并跟踪报表服务器所处理文件的有关信息。 修改任何报表服务器项的属性或设置时，改动将存储在 SharePoint 数据库中，然后被复制到向报表服务器提供内部存储的报表服务器数据库中。  
  
## <a name="related-content"></a>相关内容  
 [在 SharePoint 中激活报表服务器和 Power View 集成功能](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 描述如何激活与以前版本的报表服务器集成所需的报表服务器功能。  
  
  
