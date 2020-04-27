---
title: 服务器属性（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93365925d412f672b9e8d3e5a9b5f67a850e508a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099998"
---
# <a name="server-properties-general-page"></a>服务器属性（“常规”页）
  使用此页可以查看或修改报表管理器中所使用的标题，启用或禁用“我的报表”，为“我的报表”安全性选择角色定义以及启用或禁用客户端打印控件。  
  
 若要打开此页， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]请启动，连接到 Report Server 实例，右键单击 Report Server 名称，然后选择 "**属性**"。  
  
 服务器模式决定可以设置哪些服务器属性。 如果要管理配置为 SharePoint 集成模式的报表服务器，则不能启用“我的报表”，也不能为报表管理器设置应用程序标题。  
  
## <a name="options"></a>选项  
 **名称**  
 键入将显示在报表管理器中的应用程序名称。 此值默认为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 指定的名称仅显示在报表管理器中。  
  
 **版本**  
 此属性为只读。 指定正在使用的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的版本。  
  
 **版本(Edition)**  
 此属性为只读。 指定当前报表服务器实例。 并非 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本都提供报表管理器。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 **身份验证模式**  
 此属性为只读。 它标识报表服务器实例所接受的身份验证请求的类型。 若要更改身份验证模式，必须编辑 RSReportServer.config 文件。 有关详细信息，请参阅 [Authentication with the Report Server](../security/authentication-with-the-report-server.md)。  
  
 **URL**  
 此属性为只读。 指定报表服务器 Web 服务的 URL。 可在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具中指定此值。 有关详细信息，请参阅[配置 URL（SSRS 配置管理器）](../install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
 **为每个用户启用“我的报表”文件夹**  
 使“我的报表”可供用户使用。 此选项仅适用于处于本机模式的报表服务器。  
  
 **选择应用于每个“我的报表”文件夹的角色**  
 指定要用于“我的报表”安全性的角色定义。 角色定义标识在每个“我的报表”文件夹中都支持的任务集。  
  
 **允许下载 ActiveX 客户端打印控件**  
 设置 `EnableClientPrinting` 报表服务器系统属性。 如果启用客户端打印，则具有本地管理员权限的用户可以选择下载已签名的 ActiveX 控件来打印 HTML 报表。 有关详细信息，请参阅 [启用和禁用 Reporting Services 的客户端打印](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表服务器属性 &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [在 Management Studio 中连接到报表服务器](connect-to-a-report-server-in-management-studio.md)   
 [启用和禁用我的报表](../report-server/enable-and-disable-my-reports.md)   
 [Management Studio F1 帮助中的报表服务器](report-server-in-management-studio-f1-help.md)   
 [保护“我的报表”](../security/secure-my-reports.md)  
  
  
