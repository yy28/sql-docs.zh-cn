---
title: "服务器属性 （常规页） |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: dbd2d63c8698cb9e33361c12980aa6abdeaaae7b
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="report-server-properties-general-page"></a>报表服务器属性 （常规页）
  使用此页可以查看或修改报表管理器中所使用的标题，启用或禁用“我的报表”，为“我的报表”安全性选择角色定义以及启用或禁用客户端打印控件。  
  
 **若要打开此页，请执行以下操作：**
 1) 开始 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) 连接到报表服务器实例。
 3) 右键单击报表服务器名称，然后选择“属性”。  
  
 服务器模式决定可以设置哪些服务器属性。 如果要管理配置为 SharePoint 集成模式的报表服务器，则不能启用“我的报表”，也不能为 Web 门户设置标题。  
  
## <a name="options"></a>选项  
 **名称**  
 键入显示在 Web 门户顶部的名称。 默认情况下，此值为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 指定的名称仅显示在报表管理器中。  
  
 **版本(Version)**  
 该属性为只读。 指定所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的版本。  
  
 **版本(Edition)**  
 该属性为只读。 指定当前报表服务器实例。 并非 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本都提供报表管理器。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 **身份验证模式**  
 该属性为只读。 它标识报表服务器实例所接受的身份验证请求的类型。 若要更改身份验证模式，必须编辑 **RSReportServer.config** 文件。 有关详细信息，请参阅 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 **URL**  
 该属性为只读。 指定报表服务器 Web 服务的 URL。 可在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中指定此值。 有关详细信息，请参阅[配置 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
 **为每个用户启用“我的报表”文件夹**  
 使“我的报表”可供用户使用。 此选项仅适用于处于本机模式的报表服务器。  
  
 **选择应用于每个“我的报表”文件夹的角色**  
 指定要用于“我的报表”安全性的角色定义。 角色定义标识在每个“我的报表”文件夹中都支持的任务集。  

  
## <a name="see-also"></a>另请参阅  
 [设置报表服务器属性 (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [启用和禁用“我的报表”](../../reporting-services/report-server/enable-and-disable-my-reports.md)   
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [保护“我的报表”](../../reporting-services/security/secure-my-reports.md)  
  
  


