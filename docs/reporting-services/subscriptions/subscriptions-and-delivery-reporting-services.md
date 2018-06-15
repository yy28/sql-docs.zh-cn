---
title: 订阅和传递 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
caps.latest.revision: 56
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a3d81598480aab552b0891fb7ae1247d9149ce71
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33036914"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>订阅和传递 (Reporting Services)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅是一种配置，它在特定时间或为响应某个事件，以指定的文件格式传递报表。 例如，每周三将 MonthlySales.rdl 报表作为 Microsoft Word 文档保存至文件共享。 订阅可以用于对报表的传递（以特定报表参数值集）进行计划并使其自动完成。  
  
 你可以为单个报表创建多个订阅，以便使用不同的订阅选项；例如，可以指定不同的参数值来生成三个报表版本，如西部地区销售报表、东部地区销售和全部销售。  
  
 ![示例 SSRS 订阅流](../../reporting-services/subscriptions/media/ssrs-subscription-example-flow.png "示例 SSRS 订阅流")  
  
 并非在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供订阅。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 **本主题内容：**  
  
-   [订阅和传递应用场景](#bkmk_subscription_scenarios)  
  
-   [标准订阅和数据驱动订阅](#bkmk_standard_and_datadriven)  
  
-   [订阅要求](#bkmk_subscription_requirements)  
  
-   [传递扩展插件](#bkmk_delivery_extensions)  
  
-   [订阅的各部分](#bkmk_parts_of_subscription)  
  
-   [如何处理订阅](#bkmk_subscription_processing)  
  
-   [对订阅进行编程控制](#bkmk_code)  
  
 **本节主题：**  
  
-   [Reporting Services 中的电子邮件传递](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md) 介绍报表服务器的电子邮件传递操作和配置。  
  
-   [创建和管理本机模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) 介绍使用本机模式报表服务器创建订阅的详细步骤。  
  
-   [创建和管理 SharePoint 模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) 介绍使用 SharePoint 模式报表服务器创建订阅的详细步骤。  
  
-   [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md) 介绍报表服务器的文件共享传递操作和配置。  
  
-   [Disable or Pause Report and Subscription Processing](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)。  
  
-   [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md) 介绍到 SharePoint 库的订阅传递。  
  
-   [数据驱动订阅](../../reporting-services/subscriptions/data-driven-subscriptions.md) 提供有关使用数据驱动订阅自定义运行时报表输出的信息。  
  
-   [监视 Reporting Services 订阅](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
-   [使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> 订阅和传递应用场景  
 针对每个订阅，可以配置传递选项且可用选项由所选择的传递扩展插件决定。 传递扩展插件是支持某种分发方式的模块。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括多个传递扩展插件，传递扩展插件可以由第三方供应商提供。  
  
 如果您是开发人员，则可以创建自定义传递扩展插件，以便支持更多应用场景。 有关详细信息，请参阅 [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)。  
  
 下表对常见的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅方案进行了说明。  
  
|应用场景|Description|  
|--------------|-----------------|  
|以电子邮件形式发送报表|以电子邮件形式将报表发送给单个用户和组。 创建订阅，并指定组别名或电子邮件别名以便接收您要分发的报表。 您可以让 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在运行时确定订阅。 如果您想要将相同的报表发送给其成员会发生变化的组，则可以使用查询在运行时派生订阅列表。|  
|脱机查看报表|用户可以为订阅输出选择以下格式之一：<br /><br /> -   具有报表数据的 XML 文件<br />-   CSV（逗号分隔）<br />-   PDF<br />-   MHTML（Web 存档）<br />-   Microsoft Excel<br />-   TIFF 文件<br />-   Microsoft Word<br /><br /> 您要存档的报表可以直接发送到您计划在每天夜里备份到的共享文件夹。 要用很长时间在浏览器中加载的大型报表可通过能够在桌面应用程序中查看的格式发送到共享文件夹。|  
|预加载缓存|如果你具有参数化报表的多个实例或大量查看报表的用户，则可以在缓存中预先加载报表以便缩短需用于显示报表的处理时间。|  
|数据驱动的报表|使用数据驱动的订阅可以在运行时自定义报表输出、传递选项和报表参数设置。 订阅使用查询在运行时从数据源获取输入值。 您可以使用数据驱动订阅执行邮件合并操作，将报表发送到在处理订阅时确定的一组订户。|  
  
##  <a name="bkmk_standard_and_datadriven"></a> 标准订阅和数据驱动订阅  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支持两种类型的订阅： **标准订阅** 和 **数据驱动订阅**。 标准订阅由各个用户创建和管理。 标准订阅由静态值组成，这些值在订阅处理期间不能改变。 每个标准订阅都有一组报表显示选项、传递选项和报表参数。  
  
 数据驱动订阅通过查询外部数据源（提供用于指定收件人、报表参数或应用程序格式的值）来获取运行时订阅信息。 如果收件人列表非常大，或希望每位收件人的报表输出都不相同，则可以使用数据驱动订阅。 若要使用数据驱动订阅，必须具备生成查询的专业知识并了解如何使用参数。 通常，由报表服务器管理员创建和管理这些订阅。 有关详细信息，请参见以下内容：  
  
-   [数据驱动订阅](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
  
-   [创建数据驱动订阅（SSRS 教程）](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> 订阅要求  
 在对报表创建订阅之前，必须满足以下前提条件：  
  
|要求|Description|  
|-----------------|-----------------|  
|权限|您必须对报表具有访问权限。 在订阅报表之前，您必须具有查看该报表的权限。<br /><br /> 对于本机模式报表服务器，以下角色分配会影响订阅：<br /><br /> -   通过“管理单独的订阅”任务，用户可以创建、修改和删除特定报表的订阅。 在预定义的角色中，“浏览器”和“报表生成器”角色包括此任务。 包括此任务的角色分配只允许用户管理自己创建的那些订阅。<br />-   通过“管理所有订阅”任务，用户可以访问和修改所有订阅。 此任务是创建数据驱动订阅所必需的。 在预定义的角色中，只有“内容管理员”角色包括此任务。|  
|已存储凭据|若要创建订阅，报表必须使用已存储的凭据或不使用任何凭据在运行时检索数据。 不能订阅配置为使用当前用户的模拟凭据或委托凭据连接到外部数据源的报表。 已存储的凭据可以是 Windows 帐户或数据库用户帐户。 有关详细信息，请参阅 [为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)<br /><br /> 您必须拥有查看报表和创建单个订阅的权限。 必须对报表服务器启用 **“预定的事件和报表传递”** 。 有关详细信息，请参阅 [（旧）创建和管理本机模式报表服务器的订阅](http://msdn.microsoft.com/en-us/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)。|  
|报表中的用户依赖值|仅在标准订阅情况下，如果报表在筛选器中使用用户帐户信息或将此信息以文本形式显示在报表上，则可以对这些报表创建订阅。 在报表中，通过解析为当前用户的 **User!UserID** 表达式指定用户帐户名。 创建订阅时，将把创建订阅的用户视为当前用户。|  
|无模型项安全性|不能订阅将包含模型项安全设置的模型用作数据源的报表生成器报表。 此限制仅适用于使用模型项安全性的报表。|  
|参数值|如果报表使用参数，则必须由报表自己或在所定义的订阅中指定参数值。 如果报表中已定义了默认值，则可以将参数值设置为使用默认值。|  
  
##  <a name="bkmk_delivery_extensions"></a> 传递扩展插件  
 订阅将在报表服务器上进行处理，并且通过该服务器上部署的传递扩展插件分发。 默认情况下，可以创建将报表发送到共享文件夹或电子邮件地址的订阅。 如果将报表服务器配置为 SharePoint 集成模式，则还可以将报表发送到 SharePoint 库。  
  
 用户创建订阅后，就可以选择可用的传递扩展插件之一来确定传递报表的方式。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括以下传递扩展插件。  
  
|传递扩展插件|Description|  
|------------------------|-----------------|  
|Windows 文件共享|将报表作为静态的应用程序文件传递到可通过网络访问的共享文件夹。|  
|电子邮件|将通知或报表作为电子邮件附件或 URL 链接进行传递。|  
|SharePoint 库|将报表作为静态的应用程序文件传递到可通过 SharePoint 站点访问的 SharePoint 库。 必须将该站点与在 SharePoint 集成模式下运行的报表服务器集成。|  
|Null|Null 传递提供程序是一个专用程度很高的传递扩展插件，用于在缓存中预加载可以查看的参数化报表。此方法不能供单个订阅中的用户使用。 数据驱动订阅中的管理员可使用 Null 传递通过预加载缓存来提高报表服务器的性能。|  
  
> [!NOTE]  
>  报表传递是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 体系结构的可扩展部分。 第三方供应商可以创建自定义的传递扩展插件，将报表传送到不同的位置或设备。 有关自定义传递扩展插件的详细信息，请参阅 [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)。  
  
##  <a name="bkmk_parts_of_subscription"></a> 订阅的各部分  
 订阅定义由以下几部分组成：  
  
-   指向可在无人参与模式下运行的报表（即，使用存储凭据或不使用任何凭据的报表）的指针。  
  
-   传递方法（如电子邮件）和传递模式的设置（如电子邮件地址）。  
  
-   用于以特定格式显示报表的呈现扩展插件。  
  
-   处理订阅的条件，表现形式为事件。  
  
     通常，运行报表的条件是基于时间的。 例如，您可能想要在 UTC 时间每周二下午 3 点运行 特定的报表。 但是，如果该报表作为快照运行，则您可以指定订阅在快照刷新时运行。  
  
-   运行报表时使用的参数。  
  
     这些参数是可选的，并且仅为接受参数值的报表指定参数。 由于订阅通常由用户拥有，因此所指定的参数值因订阅而异。 例如，不同部门的销售经理将使用参数来返回本部门的数据。 所有参数都必须具有明确定义的值或有效的默认值。  
  
 订阅信息与各个报表一起存储在报表服务器数据库中。 您不能将订阅和与其相关的报表分开管理。 请注意，不能扩展订阅来使其包含说明、其他自定义文本或其他元素。 订阅只能包含上面列出的各项。  
  
##  <a name="bkmk_subscription_processing"></a> 如何处理订阅  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中包含计划和传递处理器，该处理器提供计划报表和向用户传递报表的功能。 报表服务器持续对它所监视的事件作出响应。 当发生与为某个订阅定义的条件相符的事件后，报表服务器将读取该订阅，以确定如何处理和传递报表。 报表服务器还将请求在订阅中指定的传递扩展插件。 在运行该传递扩展插件后，报表服务器将从订阅提取传递信息，再将这些信息传递给该传递扩展插件进行处理。  
  
 该传递扩展插件将以在该订阅中定义的格式呈现报表，再将报表或通知传递到指定的目标。 如果不能传递报表，则将在报表服务器日志文件中记录一个条目。 如果您希望支持重试操作，则可以对报表服务器进行配置，使其在第一次传递尝试失败后重新尝试。  
  
### <a name="processing-a-standard-subscription"></a>处理标准订阅  
 标准订阅可以生成报表的一个实例。 报表将传递到一个共享文件夹或在订阅中指定的电子邮件地址。 报表的布局和数据不发生更改。 如果报表使用参数，在处理标准订阅时报表中的每个参数都将使用单一的值。  
  
### <a name="processing-a-data-driven-subscription"></a>处理数据驱动订阅  
 数据驱动订阅可以生成可传递到多个目标的许多报表实例。 报表布局不发生改变，但如果参数值是从订阅服务器结果集传入的，报表中的数据可能会有所差异。 如果值是从行集传入的，则影响报表呈现方式的传递选项，以及确定是将报表附加在电子邮件中还是链接到电子邮件中的传递选项会因订阅服务器而异。  
  
 数据驱动订阅可以生成大量的传递。 报表服务器会为从订阅查询返回的行集中的每一行创建一个传递。  
  
### <a name="report-delivery-characteristics"></a>报表传递的特点  
 通过标准订阅传递的报表通常呈现为静态报表。 这些报表或基于最新的报表执行快照，或生成为静态报表的形式以完成传递。 如果在按需运行报表的订阅中选择 **“包括链接”** 选项，则当您单击相应的超链接时，报表服务器将运行该报表。  
  
> [!NOTE]  
>  通过 URL 传递的报表将与报表服务器保持连接，并且可以在两次查看之间进行更新或删除。 您为订阅选择的传递选项决定了是将报表以 URL 形式进行传递，还是将其嵌入到电子邮件正文中进行传递，或是作为附件发送。  
  
 在处理订阅时，可能会重新生成通过数据驱动订阅传递的报表。 报表服务器不会锁定报表的特定实例或其数据集来完成数据驱动订阅。 如果订阅针对不同的订阅者使用不同的参数值，则报表服务器将重新生成报表，以得到所需的结果。 如果在创建和传递第一个报表副本之后更新了基础数据，则在此过程中稍后获得报表的用户可能会看到基于不同结果集的数据。 您可使用以快照形式运行的报表，以确保向所有订阅者发送同一个报表实例。 然而，如果在处理订阅过程中对快照进行了计划的更新，用户仍然可能会在其报表中获得不同的数据。  
  
### <a name="triggering-subscription-processing"></a>触发订阅处理  
 报表服务器使用两种事件来触发订阅处理：一种是在计划中指定的时间驱动事件，另一种是快照更新事件。  
  
 时间驱动的触发器使用报表特定的计划或共享计划来指定订阅何时运行。 对于按需运行的报表和缓存报表而言，计划是唯一的触发选项。  
  
 快照更新事件使用报表快照的计划更新来触发订阅。 您可以根据在报表中设置的报表执行属性，定义当使用新数据更新报表时触发的订阅。  
  
##  <a name="bkmk_code"></a> 对订阅进行编程控制  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 对象模型允许你以编程方式审核和控制订阅和订阅处理。  请参阅下面的示例和快速入门︰  
  
-   [使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   有关如何使用 PowerShell 来启用和禁用订阅的示例，请参阅 [Disable or Pause Report and Subscription Processing](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)。  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
-   有关运行 PowerShell 脚本以列出所有配置为使用“文件共享帐户”的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 订阅的示例，请参阅[订阅设置和文件共享帐户 (Configuration Manager)](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据驱动订阅（SSRS 教程）](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [“计划”](../../reporting-services/subscriptions/schedules.md)   
 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [监视 Reporting Services 订阅](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
  
