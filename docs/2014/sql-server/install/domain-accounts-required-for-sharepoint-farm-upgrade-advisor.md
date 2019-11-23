---
title: SharePoint 场需要的域帐户（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c4079ea4213d7ecbec0165c32c82b3449bbb5aee
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952512"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>SharePoint 场要求使用域帐户（升级顾问）
  为场环境配置的 SharePoint 产品要求您使用域帐户。  
  
||  
|-|  
|SharePoint 模式[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **[!INCLUDE[applies](../../includes/applies-md.md)]** 。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRS](../../includes/ssrs.md)]  
  
### <a name="description"></a>描述  
 为场环境配置的 SharePoint 产品要求您使用域帐户来连接服务和数据库。 这包括您为 Reporting Services 服务帐户指定的帐户。  
  
 如果您没有对 Reporting Services 使用域用户帐户，SharePoint 2010 管理中心页及其他位置将会出现问题。 当您尝试配置 Reporting Services 集成时，将会看到类似以下内容的错误消息：  
  
 “报表服务器正在内置 NT AUTHORITY\NETWORK SERVICE 帐户下运行，而 SharePoint 场安装不支持它。 请将 Report Server 重新配置为在域帐户下运行。 "  
  
## <a name="corrective-action"></a>纠正措施  
 对于 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和以前的版本，请使用 Reporting Services 配置管理器更改分配为 Report Server 服务帐户的帐户。  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>从配置管理器中更改服务帐户  
  
1.  从 "**开始**" 菜单中，选择 "**所有程序**"，然后单击 " **Microsoft SQL Server 2008 R2**"。  
  
2.  选择 "**配置工具**"，然后单击 " **Reporting Services 配置管理器**"。  
  
3.  在 Configuration Manager 中，选择 "**服务帐户**" 选项卡。  
  
4.  选择 "**使用其他帐户**"，然后输入域帐户的凭据。  
  
5.  单击 **“应用”** 。  
  
## <a name="see-also"></a>另请参阅  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
