---
title: 管理 Reporting Services 本机模式报表服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: da2eb97e5ce57a2e6a82dda3e264b33e1e3a3b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103791"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>管理 Reporting Services 本机模式报表服务器
  本节包含使用 Reporting Services 配置管理器配置本机模式报表服务器实例的过程。  
  
## <a name="in-this-section"></a>本节内容  
 本节中的主题进行了适当分类，以便于您轻松找到所需说明。 第一部分包含有关本机模式的报表服务器的基本配置任务主题。 第二部分包含高级配置主题。 第三部分包含有关将报表服务器配置为以 SharePoint 集成模式运行的主题。  
  
### <a name="basic-configuration"></a>基本配置  
 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
 提供启动 Reporting Services 配置工具的步骤。  
  
 [配置服务帐户（SSRS 配置管理器）](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)  
 说明如何为报表服务器服务指定帐户和密码信息。  
  
 [为报表服务器注册服务主体名称 (SPN)](register-a-service-principal-name-spn-for-a-report-server.md)  
 说明如何为在使用 Kerberos 身份验证的网络上的域用户帐户下运行的报表服务器手动注册 SPN。  
  
 [配置 URL（SSRS 配置管理器）](../install-windows/configure-a-url-ssrs-configuration-manager.md)  
 说明如何建立一个或多个用于访问报表服务器 Web 服务和报表管理器的 URL。  
  
 [创建本机模式报表服务器数据库（SSRS 配置管理器）](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 提供创建报表服务器数据库的步骤。 此步骤是部署 Reporting Services 安装所必需的步骤。  
  
### <a name="advanced-or-optional-configuration"></a>高级或可选配置  
 [配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 提供配置多个报表服务器以共享报表服务器数据库的步骤。  
  
 [为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 提供有关配置报表服务器以进行电子邮件分发的步骤。  
  
 [将防火墙配置为允许报表服务器访问](configure-a-firewall-for-report-server-access.md)  
 说明如何打开用于报表服务器的入站请求和出站响应的端口。  
  
 [为本地管理配置本机模式报表服务器 (SSRS)](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 描述使用 http://localhost 连接到报表管理器或报表服务器所需的其他步骤。  
  
 [配置报表服务器以进行远程管理](configure-a-report-server-for-remote-administration.md)  
 说明如何配置远程报表服务器实例以便可以从其他计算机上连接和配置它。  
  
 [打开或关闭 Reporting Services 功能](turn-reporting-services-features-on-or-off.md)  
 说明如何删除 Reporting Services 安装中不使用的功能。  
  
 [启用远程错误 (Reporting Services)](enable-remote-errors-reporting-services.md)  
 说明如何将报表服务器上的服务器属性设置为返回有关出现在远程服务器上的错误条件的其他信息。  
  
## <a name="see-also"></a>请参阅  
 [配置和管理报表服务器（SSRS 本机模式）](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [配置和管理报表服务器（Reporting Services SharePoint 模式）](../configure-administer-report-server-reporting-services-sharepoint-mode.md)  
  
  
