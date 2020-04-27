---
title: 计划数据刷新（PowerPivot for SharePoint） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 8571208f-6aae-4058-83c6-9f916f5e2f9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 429b35f6865deb5c0c3dd79e21cfe16cac7fae91
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070011"
---
# <a name="schedule-a-data-refresh-powerpivot-for-sharepoint"></a>计划数据刷新 (PowerPivot for SharePoint)
  您可以计划数据刷新，以便自动获取对您发布到 SharePoint 站点的 Excel 工作簿内的 PowerPivot 数据的更新。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 **本主题内容：**  
  
 [先决条件](#prereq)  
  
 [数据刷新概述](#intro)  
  
 [启用并计划数据刷新](#drenablesched)  
  
 [验证数据刷新](#drverify)  
  
> [!NOTE]  
>  PowerPivot 数据刷新由 SharePoint 场中的 Analysis Services 服务器实例执行。 它与 Excel Services 中提供的数据刷新功能无关。 PowePivot 计划数据刷新功能不会刷新非 PowerPivot 数据。  
  
##  <a name="prerequisites"></a><a name="prereq"></a>先决条件  
 若要创建数据刷新计划，您必须对工作簿具有“参与讨论”或更高级别的权限。  
  
 在数据刷新过程中访问的外部数据必须可用，并且您在计划中指定的凭据必须具有访问这些数据源的权限。 计划的数据刷新要求可通过网络连接访问的数据源位置（例如，从网络文件共享而非工作站上的本地文件夹）。  
  
 该数据源不能是 Office 文档或 Access 数据库。 Office 不支持在服务器环境中使用 Office 数据连接组件。 如果您的工作簿包含来自这些数据源的数据，则请确保从您的数据刷新计划的数据源列表中删除这些资源。  
  
 工作簿必须是 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本。 如果您使用的是在早期版本的 PowerPivot for Excel 中创建的工作簿，则除非您将数据库升级到最新版本，否则计划数据刷新将不会工作。  
  
 在刷新操作完成时，必须签入工作簿。 在数据刷新结束（而非刷新开始）时，如果保存文件，针对工作簿的锁定将施加于该文件上。  
  
> [!NOTE]  
>  正在刷新数据时，服务器不会锁定工作簿。 但是，出于签入更新的文件的目的，在数据刷新结束时服务器将会锁定该文件。 此时，如果该文件已签出给其他用户，则会引发刷新后的数据。同样，如果签入该文件，但该文件明显不同于在数据刷新开始时服务器检索的副本，则刷新的数据将被丢弃。  
  
##  <a name="data-refresh-overview"></a><a name="intro"></a>数据刷新概述  
 Excel 工作簿中的 PowerPivot 可源于多种不同的外部数据源，包括您从远程服务器或网络文件共享中访问的外部数据库或数据文件。 对于包含从连接的数据源或外部数据源导入的数据的 PowerPivot 工作簿，您可以配置数据刷新以便计划自动导入这些原始数据源中更新的数据。  
  
 外部数据源是通过您在使用 PowerPivot 客户端应用程序将原始数据导入到工作簿时指定的嵌入连接字符串、URL 或 UNC 路径来访问的。 在后续的数据刷新操作中将重复使用在 PowerPivot 工作簿中存储的原始连接信息。 尽管您可以覆盖用于连接数据源的凭据，但您无法覆盖用于进行数据刷新的连接字符串；而只使用现有连接信息。  
  
 对于每个工作簿，只有一个数据刷新计划页，并且将在该页上指定所有计划信息。 通常，编写该工作簿的人员将定义该计划。  
  
 作为计划所有者，您将执行以下任务：  
  
-   定义默认计划。 这是在数据源级别未定义计划的情况下使用的计划。  
  
-   指定用于运行数据刷新的凭据  
  
-   选择要在数据刷新操作中包括的数据源。  
  
-   或者，您可以为数据刷新过程中查询的每个数据源指定内联的单独计划和凭据。 每个数据源都可以独立进行刷新。 如果您为每个数据源都创建了自定义计划，则忽略默认计划。  
  
 通过为单独数据源创建细粒度的计划，您可以使刷新计划适应外部数据源中的变动。 例如，如果外部数据源包含一整天生成的事务数据，则可以为该数据源创建单独的数据刷新计划，以便在每天夜里获取其更新的信息。  
  
##  <a name="enable-and-schedule-data-refresh"></a><a name="drenablesched"></a>启用并计划数据刷新  
 使用下面的说明可为发布到 SharePoint 库的 Excel 工作簿中的 PowerPivot 数据计划数据刷新。  
  
1.  在包含该工作簿的库中，选择该工作簿，然后单击向下箭头以显示命令列表。  
  
2.  单击 **“管理 PowerPivot 数据刷新”**。 如果已定义数据刷新计划，则您将看到“查看数据刷新历史记录”页。 您可以单击 **“配置数据刷新”** 以打开计划定义页。  
  
3.  在计划定义页中，选中 **“启用”** 复选框。  
  
4.  在“计划详细信息”中，指定计划的类型并指定其详细信息。 此步骤将创建默认计划。  
  
    > [!IMPORTANT]  
    >  请确保选中 **“也尽快刷新”** 复选框。 这样一来，您便能确认可对此工作簿进行数据刷新。 请注意，数据刷新将在您保存计划后的 1 分钟内启动。  
  
5.  在“最早开始时间”中，选择下列选项之一：  
  
    1.  **“在工作时间后”** 指定非工作时间的处理期间，在这个期间中，数据库服务器更可能收集到整个工作日所产生的最新数据。  
  
    2.  **“特定的最早开始时间”** 是您希望将数据刷新请求添加到处理队列的当日最早时分。 您可以按 15 分钟的间隔指定分钟。 这些设置会应用于当前日期和以后的日期 例如，如果您指定值为早上 6:30， 而当前时间为下午 4:30，则刷新请求将会添加到当天的队列中，因为下午 4:30 晚于早上 6:30。  
  
     最早开始时间定义何时将请求添加到处理队列。 在服务器有足够的资源开始处理数据时将发生实际处理。 处理完成后，实际的处理时间将记录在数据刷新历史记录中。  
  
6.  选中 **“也尽快刷新”** 复选框可以在服务器只要能够处理时就尽快运行数据刷新。 成功的数据刷新作业结果确认数据源是可见的并且正确设置了权限和服务器配置。  
  
7.  在“电子邮件通知”中，输入应该在发生处理错误时接到通知的人员的电子邮件地址。  
  
8.  在“凭据”中，指定用于运行数据刷新作业的帐户。 该帐户对于该工作簿必须具有“参与讨论”权限，以便可以打开该工作簿来刷新其数据。 该帐户必须是 Windows 域用户帐户。 在许多情况下，该帐户还必须对在数据刷新过程中使用的外部数据源具有读取权限。 具体来说，如果您最初使用“使用 Windows 身份验证”选项导入了数据，则将生成连接字符串以便使用当前用户的 Windows 凭据。 如果当前用户是数据刷新帐户，则该帐户必须对外部数据源具有读取权限，这样数据刷新才能成功完成。 选择以下选项之一：  
  
    1.  选择 **“使用管理员配置的数据刷新帐户”** 以使用 PowerPivot 无人参与的数据刷新帐户处理数据刷新操作。  
  
    2.  如果您希望输入用户名和密码，则选择 **“使用以下 Windows 用户凭据进行连接”** 。 以 domain\user 格式输入帐户信息。  
  
    3.  如果您知道包含您希望使用的以前存储的凭据的目标应用程序的 ID，则选择 **“使用在 Secure Store Service 中保存的凭据进行连接”** 。  
  
     有关这些选项的详细信息，请参阅为[Powerpivot 数据刷新配置存储的凭据 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)并[配置 Powerpivot 无人参与的数据刷新帐户 &#40;PowerPivot for SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。  
  
9. 如果您希望数据刷新重新查询所有原始数据源，则在“数据源”中选中 **“所有数据源”** 复选框。  
  
     如果您选中此选项，则提供 PowerPivot 数据的任何外部数据源将自动包括在刷新中，即使随着您添加或删除向工作簿提供数据的数据源，数据源列表发生变化时也是如此。  
  
     如果您想要手动选择要包括的数据源，则取消选中 **“所有数据源”** 复选框。 如果您以后通过添加新的数据源修改该工作簿，请务必在计划中更新数据源列表。 否则，较新的数据源将不会包括在刷新操作中。  
  
     当您打开工作簿的“管理 PowerPivot 数据刷新”页时，您可以从中进行选择的数据源列表是从 PowerPivot 工作簿中检索的。  
  
     请务必仅选择满足以下条件的那些数据源：  
  
    -   该数据源必须在发生数据刷新时可用，并且还必须在规定的位置上可用。 如果原始数据源处于创作此工作簿的人员的本地磁盘驱动器上，则必须或者从数据刷新操作中排除该数据源，或者确定一种方法来将该数据源发布到可通过网络连接访问的位置。 如果您将某一数据源移到某个网络位置，请确保在 [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 中打开工作簿并更新数据源连接信息。 这是重新建立 PowerPivot 工作簿中存储的连接信息所必需的。  
  
    -   必须使用嵌入在 PowerPivot 工作簿中或在计划中指定的凭据信息来访问数据源。 当您使用 PowerPivot for Excel 导入数据时，嵌入的凭据信息存储于 PowerPivot 工作簿中。 嵌入的凭据信息通常是 SSPI=IntegratedSecurity 或 SSPI=TrustedConnection，这意味着使用当前用户的凭据来连接到数据源。 如果您想要覆盖数据刷新计划中的凭据信息，则可以指定预定义的存储凭据。 有关详细信息，请参阅为[PowerPivot 数据刷新配置存储的凭据 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
    -   数据刷新必须对您指定的所有数据源均成功。 否则，刷新的数据将被放弃，只会留下上次保存的工作簿版本。 因此，请排除您不确定的任何数据源。  
  
    -   数据刷新不得使工作簿中的其他数据失效。 在您刷新您的一部分数据时，请务必了解在较新的数据与不是来自同一时间段的静态数据进行聚合后工作簿是否仍有效。 作为工作簿作者，您要知道您的数据依赖关系，并确保数据刷新适合于工作簿本身。  
  
10. 或者，您可以为特定数据源定义单独的计划。 如果您具有原始数据源，而它们本身将根据计划进行更新，则定义单独的计划将十分有用。 例如，如果 PowerPivot 数据源使用的数据来自每个星期一的 02:00 点刷新的数据市场，则可以为该数据市场定义一个内联计划，以便在每个星期一的 04:00 点检索其刷新的数据。  
  
11. 单击 **“确定”** 保存您的计划。  
  
##  <a name="verify-data-refresh"></a><a name="drverify"></a>验证数据刷新  
 验证数据刷新的最佳方式是立即执行数据刷新，然后查看历史记录页以便确定刷新是否成功完成。 对您的计划选中 **“也尽快刷新”** 复选框将提供数据刷新可正常运行的验证。  
  
 您可以在工作簿的“数据刷新历史记录”页中查看数据刷新操作的当前和过去的记录。 仅在已为工作簿计划了数据刷新后此页才出现。 如果没有数据刷新计划，将改为出现计划定义页。  
  
 您必须具有“参与讨论”权限或更高权限，才能查看数据刷新历史记录。  
  
1.  在 SharePoint 站点上，打开包含 PowerPivot 工作簿的库。  
  
     没有可视的指示器用于标识 SharePoint 库中的哪些工作簿包含 PowerPivot 数据。 您必须预先知道哪些工作簿包含可刷新的 PowerPivot 数据。  
  
2.  选择文档，然后单击显示在右侧的向下箭头。  
  
3.  选择 **“管理 PowerPivot 数据刷新”**。  
  
 此时将出现历史记录页，其中显示当前 Excel 工作簿中 PowerPivot 数据的所有刷新活动的完整记录，包括最近数据刷新操作的状态。  
  
 在某些情况下，您可能会看到实际处理时间不同于您指定的时间。 如果服务器上的处理负荷繁重，将发生此情况。 在负荷繁重的情况下， [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 服务实例将等待，直到释放了足够的系统资源后才开始数据刷新。  
  
 在刷新操作完成时，必须签入工作簿。 此时，将用刷新后的数据保存工作簿。 如果该文件已签出，则数据刷新将跳到下一计划时间。  
  
 如果您看到意外的状态消息（例如，刷新操作失败或被取消），则可以通过检查权限和服务器可用性来调查该问题。  
  
 查看 TechNet WIKI 上的 PowerPivot 数据刷新故障排除页，帮助解决数据刷新问题。 有关详细信息，请参阅 [解决 PowerPivot 数据刷新问题](https://go.microsoft.com/fwlink/?LinkId=251594)。  
  
> [!NOTE]  
>  SharePoint 管理员可通过在管理中心查看 PowerPivot 管理面板中的合并数据刷新报告来帮助您排除数据刷新问题。 有关详细信息，请参阅 [PowerPivot Management Dashboard and Usage Data](power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)。  
  
## <a name="see-also"></a>另请参阅  
 [通过 SharePoint 2010 进行 PowerPivot 数据刷新](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [查看数据刷新历史记录 &#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)   
 [为 PowerPivot 数据刷新配置存储的凭据 &#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
