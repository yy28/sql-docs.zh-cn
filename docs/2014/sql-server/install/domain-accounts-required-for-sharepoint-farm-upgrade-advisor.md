---
title: 为 SharePoint 场 （升级顾问） 所需的域帐户 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90cd6d3e-a271-4cb8-81f2-fc555b2d3cab
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: fd013ae4f7266604dde798aa76393612cd578bad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124477"
---
# <a name="domain-accounts-required-for-sharepoint-farm-upgrade-advisor"></a>SharePoint 场要求使用域帐户（升级顾问）
  为场环境配置的 SharePoint 产品要求您使用域帐户。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRS](../../includes/ssrs-md.md)]  
  
### <a name="description"></a>Description  
 为场环境配置的 SharePoint 产品要求您使用域帐户来连接服务和数据库。 这包括您为 Reporting Services 服务帐户指定的帐户。  
  
 如果您没有对 Reporting Services 使用域用户帐户，SharePoint 2010 管理中心页及其他位置将会出现问题。 当您尝试配置 Reporting Services 集成时，将会看到类似以下内容的错误消息：  
  
 “报表服务器正在内置 NT AUTHORITY\NETWORK SERVICE 帐户下运行，而 SharePoint 场安装不支持它。 请重新配置报表服务器在域帐户下运行。"  
  
## <a name="corrective-action"></a>纠正措施  
 有关[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和早期版本中，使用 Reporting Services 配置管理器更改被指定为报表服务器服务帐户的帐户。  
  
#### <a name="to-change-the-service-account-from-configuration-manager"></a>从配置管理器中更改服务帐户  
  
1.  从**启动**菜单上，选择**所有程序**，然后单击**Microsoft SQL Server 2008 R2**。  
  
2.  选择**配置工具**，然后单击**Reporting Services 配置管理器**。  
  
3.  在配置管理器中，选择**服务帐户**选项卡。  
  
4.  选择**使用另一帐户**和输入域帐户的凭据。  
  
5.  单击 **“应用”**。  
  
## <a name="see-also"></a>请参阅  
 [配置报表服务器服务帐户（SSRS 配置管理器）](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  