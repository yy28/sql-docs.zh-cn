---
title: 创建、 修改和删除标准订阅 (在本机模式下的 Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d5eadf38bcdb7573cf19941535182e2cc8f87f29
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111497"
---
# <a name="create-modify-and-delete-standard-subscriptions-reporting-services-in-native-mode"></a>Create, Modify, and Delete Standard Subscriptions (Reporting Services in Native Mode)
  标准订阅是由希望通过电子邮件传递报表或将报表传递到共享文件夹的各个用户所创建的订阅。 标准订阅始终通过其所基于的报表来定义。  
  
 创建订阅的用户拥有该订阅。 每个用户都可以修改或删除自己所拥有的订阅。  
  
> [!NOTE]  
>  从开始[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]可以以编程方式转移其所有权的订阅。 没有可用于传递订阅所有权的用户界面。 有关详细信息，请参阅 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 具体取决于**RSReportServer.config**配置文件设置，用户可能能够向订阅添加更多的用户 (例如，经理可以添加的电子邮件地址或其直接报告，以便他们会收到一份报表）。 是否支持此功能取决于在定义单独的订阅时“收件人:”字段是否可见。 有关详细信息，请参阅[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 本主题提供了由各个用户创建和管理的标准订阅的有关信息。 而数据驱动订阅具有不同的要求和步骤，将在另一个主题中进行讨论。 有关详细信息，请参阅[创建、 修改和删除数据驱动订阅](data-driven-subscriptions.md)。  
  
 本主题内容：  
  
-   [若要创建订阅](#bkmk_create_subscription)  
  
-   [创建文件共享订阅](#bkmk_create_fileshare_subscription)  
  
-   [创建电子邮件订阅](#bkmk_create_email_subscription)  
  
-   [若要修改订阅](#bkmk_modify_subscription)  
  
-   [删除订阅](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> 若要创建订阅  
 若要创建订阅，请选择对您的报表服务器部署有效的工具和方法：  
  
-   本主题中的内容说明如何使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表管理器在本机模式报表服务器上创建订阅。 定义订阅之后，可以在报表管理器中通过“我的订阅”页或特定报表的 **“订阅”** 选项卡访问订阅。  
  
-   [创建和管理 SharePoint 模式报表服务器的订阅](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)介绍了如何使用 SharePoint 站点中的应用程序页订阅在 SharePoint 集成模式下运行的报表服务器上的报表。  
  
 本主题提供创建电子邮件订阅和文件共享传递订阅的说明。  
  
-   若要使用电子邮件传递，在创建订阅之前，必须为 SMTP 服务器或网关连接配置报表服务器。  
  
-   若要使用文件共享传递，必须先定义目标文件夹。 有关详细信息，请参阅[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 必须先将报表数据源配置为使用存储的凭据或不使用凭据，然后才可以订阅报表。 有关详细信息，请参阅[在 Reporting Services 数据源中存储凭据](../report-data/store-credentials-in-a-reporting-services-data-source.md)。 否则， **“新建订阅”** 按钮将不可用。  
  
 本主题不介绍如何创建数据驱动订阅。 有关如何创建数据驱动的订阅的说明，请参阅[创建数据驱动订阅（SSRS 教程）](../create-a-data-driven-subscription-ssrs-tutorial.md)或在报表管理器中“创建数据驱动的订阅”页的联机帮助。  
  
###  <a name="bkmk_create_fileshare_subscription"></a> 创建文件共享订阅  
  
1.  启动[报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中的 **“内容”** 页上，导航到要订阅的报表。 单击报表以打开它。  
  
3.  单击 **“订阅”** 选项卡，再单击 **“新建订阅”**。  
  
4.  在 **“传递者”** 中选择 **“Windows 文件共享”**。  
  
5.  在 **“文件名”** 中，为报表键入文件名。  
  
6.  选中 **“创建文件时添加文件扩展名”**。 选择此选项，将向文件名中添加三个字符的文件扩展名。 文件扩展名由所选择的报表输出格式决定。  
  
7.  在中**路径**文字框中，键入你想要将报表传递的现有文件夹的通用命名约定 (UNC) 路径 (例如， \\ \\< servername\>\\<myreports\>)。 在路径开头包括双反斜杠字符。 在路径末尾不要使用反斜杠。  
  
8.  在“呈现格式”中，为文件传递选择一种报表输出格式。 选择与要用来打开报表的桌面应用程序相对应的格式。 避免使用不以单数据流呈现报表的格式，也不要使用引入静态文件不支持的交互的格式（例如 HTML 4.0）。  
  
9. 在“用户名”和“密码”文本框中，指定访问文件共享所需的凭据，用户名的格式为 \<domain>\\\<user name>。  
  
10. 指定覆盖选项。 如果单击 **“如果存在旧版本，则不覆盖该文件”**，则若检测到现有文件，将不进行传递。 如果单击 **“添加更新的版本时文件名递增”**，则报表服务器将在文件名末尾追加数字，以便将其与现有的同名文件区分开。  
  
11. 指定所需的报表传递时间：  
  
    -   若要计划传递时间，请单击 **“预定报表运行完成时”** ，再单击 **“选择计划”** 按钮。 将打开计划页。  
  
    -   若要选择已具有要使用的日期、时间和重复信息的预定义共享计划，请单击 **“根据共享计划”**，然后选择要使用的计划。  
  
    -   若要在报表快照更新为较新版本时传递报表，请单击“刷新报表内容时”。 如果订阅的报表以预定间隔检索数据，则用于刷新数据的计划决定处理订阅的时间。  
  
        > [!NOTE]  
        >  此选项仅适用于已与更新计划相关联的快照。  
  
12. 对于参数化报表，请指定要用于此订阅的报表的参数。 这些参数可以与用于按需运行报表的参数或其他预定操作中使用的参数不同。  
  
 报表作为静态文件传递。 如果报表包含交互功能（例如，指向其他行和列的链接），则这些功能不可用。  
  
###  <a name="bkmk_create_email_subscription"></a> 创建电子邮件订阅  
  
1.  在报表管理器中的 **“内容”** 页上，导航到要订阅的报表。 单击报表以打开它。  
  
2.  单击 **“订阅”** 选项卡，再单击 **“新建订阅”**。  
  
3.  在中**传递方式**，选择**电子邮件**。 如果此传递类型不可用，则您尚未为电子邮件订阅配置报表服务器。  
  
4.  在中**To**文本框中，在收件人的收件人姓名： 字段是使用您的域用户帐户自行填写地址。 报表服务器配置设置确定是否**到**字段是与你的用户帐户自行填写地址。 有关更改配置设置电子邮件地址的详细信息，请参阅[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
    > [!NOTE]  
    >  根据所拥有的权限，您可能还可以键入您希望报表传递到的电子邮件地址。 若要指定多个电子邮件地址，请用分号 (;) 分隔它们。 还可以在“抄送”、“密件抄送”和“答复”文本框中键入其他电子邮件地址。 这要求您具有管理所有订阅的权限。  
  
5.  按如下说明选择传递选项：  
  
    -   若要嵌入或附加报表副本，请选择 **“包括报表”**。 报表的格式由所选的呈现格式决定。 如果您认为报表大小会超过为电子邮件系统定义的限制，请不要选择此选项。  
  
    -   若要在电子邮件的正文中包括指向报表的 URL，选择**包括链接**。  
  
    > [!NOTE]  
    >  如果清除这两个选项，则将只发送“主题”行中的通知文本。  
  
6.  从 **“呈现格式”** 列表框中选择一种呈现格式。 如果选择 **“包括报表”** 以嵌入或附加报表副本，则此选项可用。  
  
    -   若要在电子邮件正文中嵌入报表，请选择“Web 存档”。  
  
    -   若要将报表作为附件发送，请选择任一其他呈现格式。  
  
7.  从 **“优先级”** 列表框中选择优先级。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 中，此设置可为电子邮件的重要性级别设置标志。  
  
8.  指定所需的报表传递时间：  
  
    -   若要计划传递时间，请单击 **“预定报表运行完成时”** ，再单击 **“选择计划”**。 将打开计划页。  
  
    -   若要选择已具有要使用的日期、时间和重复信息的预定义共享计划，请单击 **“根据共享计划”**，然后选择要使用的计划。  
  
    -   若要在报表快照更新为较新版本时传递报表，请单击“刷新报表内容时”。 如果订阅的报表以预定间隔检索数据，则用于刷新数据的计划决定处理订阅的时间。  
  
    > [!NOTE]  
    >  此选项仅适用于已与更新计划相关联的快照。  
  
9. 对于参数化报表，请指定要用于此订阅的报表的参数。 这些参数可以与用于按需运行报表的参数或其他预定操作中使用的参数不同。  
  
##  <a name="bkmk_modify_subscription"></a> 若要修改订阅  
 您可以随时修改订阅。 在修改正在处理的订阅时，如果更新的设置在传递扩展插件接收订阅数据之前就已保存到报表服务器数据库中，则订阅将使用更新的设置。 否则，使用现有设置。  
  
 若要定位订阅，请使用 **“我的订阅”** 页或查看与报表关联的订阅定义。 您既不能直接搜索订阅，也不能根据所有者名称、触发器信息、状态信息等来搜索订阅。  
  
 订阅还可以由报表服务器管理员来修改或删除。  
  
> [!NOTE]  
>  报表服务器管理员无法从一个位置管理在给定的报表服务器上正在使用的所有单独的订阅。 但是，报表服务器管理员可以访问每个单独的订阅来进行修改或删除。  
  
##  <a name="bkmk_delete_subscription"></a> 删除订阅  
 删除订阅  
  
1.  启动[报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器的全局工具栏上，单击 **“我的订阅”** ，并导航到要修改或删除的订阅。  
  
3.  或者，在打开的报表的 **“订阅”** 选项卡上找到要修改或删除的订阅。 执行下列操作之一：  
  
    1.  若要修改订阅，请单击 **“编辑”**。  
  
    2.  若要删除订阅，请选中订阅旁边的复选框，再单击 **“删除”**。  
  
 本主题不介绍如何取消报表服务器上当前正在处理的订阅。 有关取消订阅的详细信息，请参阅[管理正在运行的进程](manage-a-running-process.md)  
  
 如果您想终止某个订阅，但又无法轻松地定位该订阅，请记下正在接收的报表，然后按名称搜索该报表。 在访问该报表之后，您就可以从订阅中删除订阅本身。 如果找不到该订阅，则该订阅可能是数据驱动订阅。 有关详细信息，请咨询报表服务器管理员。  
  
 如果删除了基础报表，则将自动删除订阅。 在删除正在处理的订阅时，如果在传递扩展插件接收订阅数据之前执行删除操作，则该订阅将停止。 否则，将继续处理该订阅。  
  
## <a name="see-also"></a>请参阅  
 [任务和权限](../security/tasks-and-permissions.md)   
 [创建和管理 SharePoint 模式报表服务器的订阅](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [创建和管理本机模式报表服务器的订阅](../create-manage-subscriptions-native-mode-report-servers.md)   
 [数据驱动订阅](data-driven-subscriptions.md)   
 [订阅和传递&#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [报表管理器&#40;SSRS 本机模式&#41;](../report-manager-ssrs-native-mode.md)   
 [使用我的订阅](use-my-subscriptions-native-mode-report-server.md)  
  
  
