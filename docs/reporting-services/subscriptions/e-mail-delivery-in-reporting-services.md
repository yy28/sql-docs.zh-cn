---
title: "Reporting Services 中的电子邮件传递 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 89246a976a0de3c1f3c3581509cb0f71a26cd1a5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services 中的电子邮件传递
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中包含电子邮件传递扩展插件，该插件提供了通过电子邮件将报表发送到单个用户或组的方式。 若要通过电子邮件分发报表，你可以 1) 配置报表服务器以进行电子邮件传递，并 2) 定义标准订阅或数据驱动订阅。 一个订阅不能在一个电子邮件中传递多个报表。 但你可以创建多个订阅。  
  
 报表服务器通过标准连接与电子邮件服务器相连。 它不使用通过安全套接字层 (SSL) 进行加密的通信。 电子邮件服务器必须是与报表服务器位于同一网络上的远程或本地简单邮件传输协议 (SMTP) 服务器。  
  
 有关指导你创建订阅的详细步骤，请参阅以下内容：  
  
-   [创建和管理本机模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [创建和管理 SharePoint 模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
## <a name="e-mail-delivery-options"></a>电子邮件传递选项  
 报表服务器电子邮件传递可以通过以下方式传递报表  
  
-   将通知和超链接发送到所生成的报表。  
  
-   在电子邮件的“主题:”行中发送通知。 默认情况下，订阅定义中的“主题:”行包含以下变量（这些变量将在处理订阅时替换为报表特定的信息）：  
  
     **@ReportName** 指定报表的名称。  
  
     **@ExecutionTime** 指定执行报表的时间。  
  
     您可以将这些变量与静态文本组合在一起，也可以修改每个订阅的“主题:”行中的文本。  
  
-   发送嵌入或作为附件的报表。 呈现格式和浏览器决定了报表是嵌入的还是作为附件发送。  
  
     如果您的浏览器支持 HTML 4.0 和 MHTML，并且您选择了 Web 存档呈现格式，那么报表将嵌入为邮件的一部分。 其他所有呈现格式（CSV、PDF 等）都将报表作为附件进行传递。 对于本机模式的报表服务器，你可以在 RSReportServer.config 配置文件中禁用此功能。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不会检查附件或邮件的大小。 如果附件或邮件的大小超出邮件服务器允许的最大限制，则无法传递报表。 如果是大型报表，请选择其他传递选项（例如 URL 或通知）。  
  
 在您创建订阅时，将设置确定报表传递方式的传递选项。 例如，如果选择在订阅中“包含链接”，电子邮件将包含一个指向该报表的超链接。  
  
## <a name="native-mode-role-based-e-mail-settings"></a>本机模式的基于角色的电子邮件设置  
 在本机模式的报表服务器环境中，所使用的电子邮件传递设置因角色是包含“管理单独的订阅”任务还是“管理所有订阅”任务而异。  
  
|任务|可用设置|  
|----------|------------------------|  
|管理单独的订阅|显示使用户能够向自己自动传递报表的字段。 在此模式下，接受电子邮件别名的字段不可用。|  
|管理所有订阅|显示支持更大分发范围的字段，包括“收件人:”字段、“抄送:”字段、“密件抄送:”字段和“答复:”字段，从而提供了另外一些向更多订阅者发送报表的方法。 电子邮件别名字段的可用性是通过 RSReportServer 配置文件设置进行定义的。|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>在订阅中指定电子邮件地址  
 如果您是在 Intranet 内分发报表，并且使用的是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 服务器的 SMTP 网关，则键入电子邮件别名（就像给同事发送电子邮件一样）。 如果传递的目标是外部电子邮件帐户，则键入完整的电子邮件地址。 如果您指定更多电子邮件地址，以便将其他人添加到订阅中，则这些订阅者将获得与从该订阅生成的报表完全相同的副本。  
  
 报表服务器不验证电子邮件地址或从电子邮件服务器获得电子邮件地址。 您事先必须知道要使用哪些电子邮件地址。 默认情况下，您可以通过电子邮件将报表发送到组织内外任何有效的电子邮件帐户。 不过，您可以使用配置设置限制将电子邮件传递到通过名称标识的特定邮件服务器主机。 如果您希望支持以电子邮件方式向组织外的人员传递报表，则可以指定其他主机。  
  
 必须通过在电子邮件服务器上定义的电子邮件帐户来发送用于传递报表的电子邮件。 其中一项配置设置指定此电子邮件帐户。 该电子邮件帐户适用于通过电子邮件传递扩展插件传递的所有报表；您不能指定多个帐户或针对单个报表更改这一帐户。  
  
## <a name="controlling-e-mail-delivery"></a>控制电子邮件传递  
 您可以配置报表服务器，使电子邮件分发仅限于特定主机域。 例如，可以阻止本机报表服务器将报表传递到所有域，而只传递到 **RSReportServer.config** 配置文件所列出的域。  
  
 还可以设置配置设置，以在订阅中隐藏 **“收件人”** 字段。 在这种情况下，报表只能传递给定义订阅的用户。 但是，报表发送给用户后，您无法有效地防止转发报表。  
  
 控制报表分发的最有效的方式是，将报表服务器配置为只发送报表服务器 URL。 报表服务器使用 Windows 身份验证和基于角色的授权模型来控制报表的访问权限。 如果用户意外地通过电子邮件收到无权查看的报表，报表服务器不会显示该报表。 有关订阅的详细信息，请参阅以下内容。  
  
## <a name="e-mail-server-configuration"></a>电子邮件服务器配置  
 对于本机模式的报表服务器，电子邮件传递扩展插件通过本机模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器和编辑 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置文件进行配置。 对于 SharePoint 模式的报表服务器，电子邮件传递扩展插件是在 SharePoint 管理页和 PowerShell 脚本中进行配置的。  
  
 
 有关如何配置本机模式报表服务器的信息，请参阅[电子邮件设置 - Reporting Services 本机模式（配置管理器）](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)
 
 
 有关如何配置 SharePoint 模式报表服务器的信息，请参阅以下内容：  
  
  
## <a name="see-also"></a>另请参阅  
 [任务和权限](../../reporting-services/security/tasks-and-permissions.md)   
 [订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [数据驱动订阅](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [角色分配](../../reporting-services/security/role-assignments.md)  
  
  
