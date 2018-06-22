---
title: 报表服务器 （升级顾问） 上检测到自定义扩展 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4ae9dbac7395e44bf67731bd0e7a714c73fac296
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016084"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>在报表服务器上检测到自定义扩展插件（升级顾问）
  升级顾问在配置文件中检测到自定义扩展插件设置，这说明您的安装包括一个或多个用于进行数据处理、传递、呈现、安全或身份验证的自定义扩展插件。 升级操作将移动被升级的报表服务器上的扩展插件配置设置。 但是，如果在现有报表服务器安装文件夹中安装了自定义扩展插件，则这些自定义扩展插件的程序集文件不会在升级过程期间移动到新安装文件夹。 在升级完成之后，必须将程序集文件移动到新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装文件夹。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供允许开发人员创建数据处理、 传递、 呈现、 安全性和身份验证的自定义扩展的可扩展体系结构。  
  
 如果在您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中使用自定义扩展插件或程序集，则可以使用安装程序执行升级，但可能需要在升级完成之后将扩展插件移动到新的安装位置，否则可能需要在升级之前执行相应步骤。  
  
> [!NOTE]  
>  升级顾问未检测到是否配置了用于在报表中计算项值、样式和格式的自定义代码程序集。 有关详细信息，请参阅[其他 Reporting Services 升级问题](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)。  
  
 如果购买了某个软件供应商的自定义扩展插件，请向供应商索取有关升级自定义功能的其他信息。  
  
## <a name="corrective-action"></a>纠正措施  
 使用以下几节可以确定除了执行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的升级以外或在执行该操作之前要执行的步骤：  
  
 [自定义数据处理或传递扩展插件](#dataprocdeliver)  
  
 [自定义呈现扩展插件](#render)  
  
 [SQL Server 2000 报表服务器上的自定义安全或身份验证扩展](#secauth2000)  
  
 [SQL Server 2005 报表服务器上的自定义安全或身份验证扩展](#secauth2005)  
  
 在升级完成之后，请将扩展程序集移动到新安装文件夹，然后验证自定义扩展插件是否可按期望工作。 如果扩展插件不工作，则可能必须重新编译它。  
  
#### <a name="to-recompile-an-extension"></a>重新编译扩展插件  
  
1.  将 Microsoft.ReportingServices.Interfaces.dll 文件复制到包含源代码的文件夹中。  
  
2.  打开包含源文件的项目，并添加对 Microsoft.ReportingServices.Interfaces.dll 文件的引用。  
  
3.  重新生成解决方案以绑定扩展插件。  
  
 如果决定不继续升级，则可能决定转而迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 有关迁移的自定义扩展的步骤，请参阅[迁移自定义扩展](#migrcustext)本主题中。  
  
###  <a name="dataprocdeliver"></a> 自定义数据处理或传递扩展插件  
 如果升级顾问检测到自定义数据处理或传递扩展插件，则不阻塞升级过程。 但是，在升级完成之后，可能需要先执行其他步骤，然后这些扩展插件提供的自定义功能才能工作。 例如，在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装文件夹中安装自定义扩展插件文件时，必须执行其他步骤。  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>自定义数据处理或传递扩展插件的升级后步骤  
  
1.  将扩展插件文件移动到报表服务器的新程序文件夹。 默认情况下，报表服务器程序文件夹位于 files\microsoft SQL Server\MSRS10_50。\< *instance_name*> \report 服务器。  
  
 有关详细信息，请参阅 SQL Server 联机丛书中的“部署数据处理扩展插件”和“实现传递扩展插件”。  
  
###  <a name="render"></a> 自定义呈现扩展插件  
 如果升级顾问检测到自定义呈现扩展插件，则阻塞升级过程。 通过从配置文件中删除自定义扩展插件配置项，可以继续执行升级过程。 但是，这将导致在升级完成之后自定义扩展插件对用户不可用。 如果需要在升级之后自定义呈现扩展插件，必须生成更新的呈现扩展插件，或从自定义扩展插件供应商那里获得更新的呈现扩展插件。  
  
 必须执行相应步骤才能启用升级，否则可能选择迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
> [!IMPORTANT]  
>  请在已测试并验证更新的呈现扩展插件可以按期望工作后，才升级或迁移报表服务器。  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>升级自定义呈现扩展插件  
  
1.  获得带有最新接口的呈现扩展插件。  
  
2.  从 RSReportServer.config 删除旧的自定义呈现扩展插件项。  
  
3.  升级报表服务器。  
  
4.  在升级完成之后，请在报表服务器上安装更新的扩展插件。  
  
 有关详细信息，请参阅 SQL Server 联机丛书中的“实现呈现扩展插件”。  
  
###  <a name="secauth2000"></a> SQL Server 2000 报表服务器上的自定义安全或身份验证扩展  
 如果升级顾问在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 报表服务器上检测到自定义安全或身份验证扩展插件，则阻塞升级过程。 必须执行相应步骤才能启用升级，否则可能选择迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 在两种情况下，都必须用 Microsoft.ReportingServices.Interfaces.dll 中的最新接口以更新和重新编译扩展插件，因为此接口已在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之间发生更改。  
  
> [!IMPORTANT]  
>  请在已测试并验证更新的安全或身份验证扩展插件可以按期望工作之后，才升级或迁移报表服务器。  
  
 如果使用的是为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 创建的自定义身份验证扩展插件，则必须修改源代码以支持为模型驱动报表引入的新的类和成员。  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>若要升级的 SQL Server 2000 报表服务器中的自定义的安全或身份验证扩展  
  
1.  用最新接口更新并重新编译任何安全或身份验证扩展插件。  
  
2.  从 RSReportServer.config 删除安全或身份验证扩展插件项。  
  
3.  升级报表服务器。  
  
4.  在升级完成之后，请在报表服务器上安装更新的扩展插件。  
  
 有关详细信息，请参阅 SQL Server 联机丛书中的“实现安全扩展插件”。  
  
###  <a name="secauth2005"></a> SQL Server 2005 报表服务器上的自定义安全或身份验证扩展  
 如果升级顾问在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 报表服务器上检测到自定义安全或身份验证扩展插件，则阻塞升级过程。 必须执行相应步骤才能启用升级，否则可能选择迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>从 SQL Server 2005 报表服务器升级自定义安全或身份验证扩展插件  
  
1.  从 RSReportServer.config 删除安全或身份验证扩展插件配置项。  
  
2.  升级报表服务器。  
  
3.  升级完成之后，请在 RSReportServer.config 中添加配置项。  
  
4.  如果将扩展程序集安装在旧的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装文件夹中，请将它们移动到新安装文件夹。  
  
 有关详细信息，请参阅 SQL Server 联机丛书中的“实现安全扩展插件”。  
  
###  <a name="migrcustext"></a> 迁移自定义扩展  
 如果决定迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 而不执行升级，请执行相应步骤将自定义扩展插件迁移到新 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>将自定义扩展插件迁移到新报表服务实例  
  
1.  生成或获得带有最新 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 接口的更新的扩展插件。  
  
2.  将报表服务器迁移到新实例。  
  
3.  在新实例上配置扩展插件。  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 升级问题&#40;升级顾问&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  