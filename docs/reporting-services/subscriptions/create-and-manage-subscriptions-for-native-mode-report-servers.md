---
title: 创建和管理本机模式报表服务器的订阅 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fc05bd786594cc70836bc6d39e86143d16089979
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617435"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>创建和管理本机模式报表服务器的订阅
  标准订阅是由希望通过电子邮件传递报表或将报表传递到共享文件夹的各个用户所创建的订阅。 本主题提供了由各个用户创建和管理的标准订阅的有关信息。 而数据驱动订阅具有不同的要求和步骤，将在另一个主题中进行讨论。 有关详细信息，请参阅 [创建、修改和删除数据驱动订阅](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
  
 **本主题内容：**  
  
-   [针对订阅的一般要求](#bkmk_create_subscription)  
  
-   [创建文件共享订阅](#bkmk_create_fileshare_subscription)  
  
-   [创建电子邮件订阅](#bkmk_create_email_subscription)  
  
-   [修改订阅](#bkmk_modify_subscription)  
  
-   [删除订阅](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> 针对订阅的一般要求  
 本主题中的内容说明如何使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表管理器在本机模式报表服务器上创建订阅。 定义订阅之后，可以在报表管理器中通过“我的订阅”页或特定报表的 **“订阅”** 选项卡访问订阅。  
  
 [创建和管理 SharePoint 模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) 介绍了如何使用 SharePoint 站点中的应用程序页订阅在 SharePoint 模式下运行的报表服务器上的报表。  
  
-   若要使用电子邮件传递，在创建订阅之前，必须为 SMTP 服务器或网关连接配置报表服务器。  
  
-   若要使用文件共享传递，必须先定义目标文件夹。 有关详细信息，请参阅[为报表服务器配置电子邮件传递（SSRS 配置管理器）](http://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
 必须先将报表数据源配置为使用存储的凭据或不使用凭据，然后才可以订阅报表。 有关详细信息，请参阅 [在 Reporting Services 数据源中存储凭据](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)。 否则， **“新建订阅”** 按钮将不可用。  
  
 本主题不介绍如何创建数据驱动订阅。 有关如何创建数据驱动的订阅的说明，请参阅[创建数据驱动订阅（SSRS 教程）](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)或在报表管理器中“创建数据驱动的订阅”页的联机帮助。  
  
###  <a name="bkmk_create_fileshare_subscription"></a> 创建文件共享订阅  
  
1.  启动 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  导航到你要订阅的报表。 单击报表菜单，然后单击“订阅” 。  
  
     ![报表菜单](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "report menu")  
  
3.  **描述**：键入此报表的描述，最多 512 个字符。  
  
4.  **所有者**：“所有者”字段默认为当前用户，创建订阅时不能编辑。 但是，在保存订阅后，你可以更改订阅属性，包括所有者和描述。  
  
5.  **传递方式**：选择“Windows 文件共享” 。  
  
6.  **文件名**：键入报表的文件名。  
  
7.  **创建文件时添加文件扩展名**：此选项会在文件名中添加三个字符的文件扩展名。 文件扩展名由所选择的报表输出格式决定。  
  
8.  **路径**：键入要向其中传递报表的现有文件夹的通用命名约定 (UNC) 路径（例如，\\\\<servername\>\\<myreports\>）。 在路径开头包括双反斜杠字符。 在路径末尾不要使用反斜杠。  
  
     ![文件共享订阅](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "file share subscription")  
  
9. **呈现格式**：为文件传递选择一种报表输出格式。 选择与要用来打开报表的桌面应用程序相对应的格式。 避免使用不以单数据流呈现报表的格式，也不要使用引入静态文件不支持的交互的格式（例如 HTML 4.0）。  
  
10. **凭据**：选择使用文件共享帐户或特定的 Windows 用户凭据。 如果你的报表管理员尚未配置文件共享帐户，则将禁用“使用文件共享帐户”  。 有关详细信息，请参阅[订阅设置和文件共享帐户 (Configuration Manager)](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)。 在“用户名”和“密码”文本框中，指定访问文件共享所需的凭据，用户名的格式为 \<domain>\\\<user name>。  
  
11. **覆盖选项**：  
  
    -   **如果存在旧版本，则不覆盖文件**，如果检测到现有文件，将不进行传递。  
  
    -   **添加较新的版本时文件名递增**，报表服务器将在文件名末尾追加数字，以便将其与现有的同名文件区分开。  
  
12. **计划**：指定报表的传递时间：  
  
    -   若要计划传递时间，请单击 **“预定报表运行完成时”** ，再单击 **“选择计划”** 按钮。 将打开计划页。  
  
    -   若要选择已具有要使用的日期、时间和重复信息的预定义共享计划，请单击 **“根据共享计划”**，然后选择要使用的计划。  
  
    -   若要在报表快照更新为较新版本时传递报表，请单击“刷新报表内容时”。 如果订阅的报表以预定间隔检索数据，则用于刷新数据的计划决定处理订阅的时间。  
  
        > [!NOTE]  
        >  此选项仅适用于已与更新计划相关联的快照。  
  
13. 对于参数化报表，请指定要用于此订阅的报表的参数。 这些参数可以与用于按需运行报表的参数或其他预定操作中使用的参数不同。  
  
 报表作为静态文件传递。 如果报表包含交互功能（例如，指向其他行和列的链接），则这些功能不可用。  
  
###  <a name="bkmk_create_email_subscription"></a> 创建电子邮件订阅  
  
1.  启动 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  导航到你要订阅的报表。 单击报表菜单，然后单击“订阅” 。  
  
     ![报表菜单](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "report menu")  
  
3.  **描述**：键入此报表的描述，最多 512 个字符。  
  
4.  **所有者**：“所有者”字段默认为当前用户，创建订阅时不能编辑。 但是，在保存订阅后，你可以更改订阅属性，包括所有者和描述。  
  
5.  **传递方式**：选择“电子邮件”。 如果“电子邮件”不可用，说明尚未为电子邮件订阅配置报表服务器。 请参阅[为报表服务器配置电子邮件传递（SSRS 配置管理器）](http://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)  
  
6.  **收件人**：“收件人:”字段中的收件人姓名会使用你的域用户帐户自行填写地址。 确认其格式为 [用户名]@[domain.com] 报表服务器配置设置将决定“收件人”字段是否使用用户帐户自行填写地址。 若要详细了解如何更改配置设置的电子邮件地址，请参阅[为报表服务器配置电子邮件传递（SSRS 配置管理器）](http://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
    > [!NOTE]  
    >  根据所拥有的权限，您可能还可以键入您希望报表传递到的电子邮件地址。 若要指定多个电子邮件地址，请用分号 (;) 分隔它们。 还可以在“抄送”、“密件抄送”和“答复”文本框中键入其他电子邮件地址。 这要求您具有管理所有订阅的权限。  
  
7.  ：默认为“在 @ExecutionTime 执行 @ReportName”。 可以对主题进行编辑，但请注意，@ReportName 和 @ExecutionTime 是“主题”字段中仅支持的两个全局变量。  
  
8.  按如下说明选择传递选项：  
  
    -   **包括报表**：选择此选项可嵌入或附加报表副本。 报表的格式由所选的呈现格式决定。 如果您认为报表大小会超过为电子邮件系统定义的限制，请不要选择此选项。  
  
    -   **包括链接**：选择此选项可在电子邮件正文中包括指向报表的 URL 链接。  
  
    > [!NOTE]  
    >  如果清除这两个选项，则将只发送“主题”行中的通知文本。  
  
9. 从 **“呈现格式”** 列表框中选择一种呈现格式。 如果选择 **“包括报表”** 以嵌入或附加报表副本，则此选项可用。  
  
    -   若要在电子邮件正文中嵌入报表，请选择“Web 存档”。  
  
    -   若要将报表作为附件发送，请选择任一其他呈现格式。  
  
10. 从 **“优先级”** 列表框中选择优先级。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 中，此设置可为电子邮件的重要性级别设置标志。  
  
11. 指定所需的报表传递时间：  
  
    -   若要计划传递时间，请单击 **“预定报表运行完成时”** ，再单击 **“选择计划”**。 将打开计划页。  
  
    -   若要选择已具有要使用的日期、时间和重复信息的预定义共享计划，请单击 **“根据共享计划”**，然后选择要使用的计划。  
  
    -   若要在报表快照更新为较新版本时传递报表，请单击“刷新报表内容时”。 如果订阅的报表以预定间隔检索数据，则用于刷新数据的计划决定处理订阅的时间。  
  
    > [!NOTE]  
    >  此选项仅适用于已与更新计划相关联的快照。  
  
12. 对于参数化报表，请指定要用于此订阅的报表的参数。 这些参数可以与用于按需运行报表的参数或其他预定操作中使用的参数不同。  
  
##  <a name="bkmk_modify_subscription"></a> 修改订阅  
 您可以随时修改订阅。 在修改正在处理的订阅时，如果更新的设置在传递扩展插件接收订阅数据之前就已保存到报表服务器中，则订阅将使用更新的设置。 否则，使用现有设置。  
  
 创建订阅的用户拥有该订阅。 每个用户都可以修改或删除自己所拥有的订阅。 你可以从订阅属性页中更改报表的所有者，或者以编程方式更改所有权。 有关详细信息，请参见以下内容：  
  
-   [使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 若要定位订阅，请使用 **“我的订阅”** 页或查看与报表关联的订阅定义。 您既不能直接搜索订阅，也不能根据所有者名称、触发器信息、状态信息等来搜索订阅。  
  
 订阅还可以由报表服务器管理员来修改或删除。  
  
> [!NOTE]  
>  报表服务器管理员无法从一个位置管理在给定的报表服务器上正在使用的所有单独的订阅。 但是，报表服务器管理员可以访问每个单独的订阅来进行修改或删除。  
  
##  <a name="bkmk_delete_subscription"></a> 删除订阅  
 删除订阅  
  
1.  启动 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  在报表管理器的工具栏上，单击“我的订阅”  ，并导航到要修改或删除的订阅。  
  
3.  单击报表菜单，然后单击“删除”   
  
     ![报表菜单](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "report menu")  
  
 若要取消报表服务器上当前正在处理的订阅，请参阅 [管理运行中的进程](../../reporting-services/subscriptions/manage-a-running-process.md)。  
  
 如果你想终止某个订阅，但又无法定位该订阅，请记下要接收的报表，然后按名称搜索该订阅。 在访问该报表之后，您就可以从订阅中删除订阅本身。 如果找不到该订阅，则该订阅可能是数据驱动订阅。 有关详细信息，请咨询报表服务器管理员。  
  
 如果删除了基础报表，则将自动删除订阅。 在删除正在处理的订阅时，如果在传递扩展插件接收订阅数据之前执行删除操作，则该订阅将停止。 否则，将继续处理该订阅。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理 SharePoint 模式报表服务器的订阅](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [数据驱动订阅](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [使用我的订阅（本机模式报表服务器）](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
  
  
