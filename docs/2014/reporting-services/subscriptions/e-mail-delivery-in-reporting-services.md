---
title: Reporting Services 中的电子邮件传递 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 45e72fe3c163f05f283965beb5fb3cf6ce62c50e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59957653"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services 中的电子邮件传递
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中包含电子邮件传递扩展插件，该插件提供了通过电子邮件将报表发送到单个用户或组的方式。 电子邮件传递扩展插件是通过 Reporting Services 配置管理器并编辑 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置文件进行配置的。  
  
 若要通过电子邮件分发或接收报表，请定义标准订阅或数据驱动订阅。 您一次只能订阅或分发一个报表。 您不能创建在一个电子邮件中传递多个报表的订阅。 有关订阅的详细信息，请参阅[创建、 修改和删除标准订阅&#40;本机模式下的 Reporting Services&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式下&#124;SharePoint 2010 和 SharePoint 2013<br /><br /> **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式|  
  
## <a name="e-mail-delivery-options"></a>电子邮件传递选项  
 报表服务器电子邮件传递可以通过以下方式传递报表：  
  
-   将通知和超链接发送到所生成的报表。  
  
-   在电子邮件的“主题:”行中发送通知。 默认情况下，订阅定义中的“主题:”行包含以下变量（这些变量将在处理订阅时替换为报表特定的信息）：  
  
     **@ReportName** 指定报表的名称。  
  
     **@ExecutionTime** 指定执行报表的时间。  
  
     您可以将这些变量与静态文本组合在一起，也可以修改每个订阅的“主题:”行中的文本。  
  
-   发送嵌入或作为附件的报表。 呈现格式和浏览器决定了报表是嵌入的还是作为附件发送。  
  
     如果您的浏览器支持 HTML 4.0 和 MHTML，并且您选择了 Web 存档呈现格式，那么报表将嵌入为邮件的一部分。 其他所有呈现格式（CSV、PDF 等）都将报表作为附件进行传递。 您可以在 RSReportServer 配置文件中禁用此功能。  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不会检查附件或邮件的大小。 如果附件或邮件的大小超出邮件服务器允许的最大限制，则无法传递报表。 如果是大型报表，请选择其他传递选项（例如 URL 或通知）。  
  
 在您创建订阅时，将设置确定报表传递方式的传递选项。 例如，如果选择在订阅中“包含链接”，电子邮件将包含一个指向该报表的超链接。  
  
## <a name="role-based-e-mail-settings"></a>基于角色的电子邮件设置  
 订阅报表时，根据您的角色中包含的是“管理单独的订阅”任务，还是“管理所有订阅”任务，您所使用的电子邮件传递设置将有所不同。  
  
|任务|可用设置|  
|----------|------------------------|  
|管理单独的订阅|显示使用户能够向自己自动传递报表的字段。 在此模式下，接受电子邮件别名的字段不可用。|  
|管理所有订阅|显示支持更大分发范围的字段，包括“收件人:”字段、“抄送:”字段、“密件抄送:”字段和“答复:”字段，从而提供了另外一些向更多订阅者发送报表的方法。 电子邮件别名字段的可用性是通过 RSReportServer 配置文件设置进行定义的。|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>在订阅中指定电子邮件地址  
 如果您是在 Intranet 内分发报表，并且使用的是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 服务器的 SMTP 网关，则键入电子邮件别名（就像给同事发送电子邮件一样）。 如果传递的目标是外部电子邮件帐户，则键入完整的电子邮件地址。 如果您指定更多电子邮件地址，以便将其他人添加到订阅中，则这些订阅者将获得与从该订阅生成的报表完全相同的副本。  
  
 报表服务器不验证电子邮件地址或从电子邮件服务器获得电子邮件地址。 您事先必须知道要使用哪些电子邮件地址。 默认情况下，您可以通过电子邮件将报表发送到组织内外任何有效的电子邮件帐户。 不过，您可以使用配置设置限制将电子邮件传递到通过名称标识的特定邮件服务器主机。 如果您希望支持以电子邮件方式向组织外的人员传递报表，则可以指定其他主机。  
  
 必须通过在电子邮件服务器上定义的电子邮件帐户来发送用于传递报表的电子邮件。 其中一项配置设置指定此电子邮件帐户。 该电子邮件帐户适用于通过电子邮件传递扩展插件传递的所有报表；您不能指定多个帐户或针对单个报表更改这一帐户。  
  
## <a name="e-mail-server-configuration"></a>电子邮件服务器配置  
 报表服务器通过标准连接与电子邮件服务器相连。 它不使用通过安全套接字层 (SSL) 进行加密的通信。 电子邮件服务器必须是与报表服务器位于同一网络上的远程或本地简单邮件传输协议 (SMTP) 服务器。  
  
 有关如何配置本机模式报表服务器的信息，请参阅以下内容：  
  
-   [为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
  
-   [电子邮件设置-配置管理器&#40;SSRS 本机模式&#41;](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)  
  
 有关如何配置 SharePoint 模式报表服务器的信息，请参阅以下内容：  
  
-   [为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013）](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)  
  
## <a name="see-also"></a>请参阅  
 [任务和权限](../security/tasks-and-permissions.md)   
 [订阅和传递 (Reporting Services)](subscriptions-and-delivery-reporting-services.md)   
 [数据驱动订阅](data-driven-subscriptions.md)   
 [角色分配](../security/role-assignments.md)  
  
  
