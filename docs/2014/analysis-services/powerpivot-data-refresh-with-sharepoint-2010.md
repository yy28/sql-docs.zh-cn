---
title: 使用 SharePoint 2010 的 PowerPivot 数据刷新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 01b54e6f-66e5-485c-acaa-3f9aa53119c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3d385ae733c44e403ba9de412c0c2a3e0eacd3c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365549"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2010"></a>使用 SharePoint 2010 进行 PowerPivot 数据刷新
  [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 数据刷新是在服务器端计划的操作，它对外部数据源进行查询以便更新在内容库中存储的 Excel 2010 工作簿中嵌入的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 数据。  
  
 数据刷新是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 的内置功能，但使用该功能要求您在 SharePoint 2010 场中运行特定的服务和计时器作业。 为使数据刷新成功，通常还要求执行其他一些管理步骤，例如安装数据访问接口和检查数据库权限。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 和 SharePoint Server 2013 Excel Services 将不同的体系结构用于 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 数据模型的数据刷新。 新的体系结构利用 Excel Services 作为主要组件加载 PowerPivot 数据模型。 以前的数据刷新体系结构依赖在 SharePoint 模式下运行 PowerPivot 系统服务和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的服务器来加载数据模型。 有关详细信息，请参阅[使用 SharePoint 2013 的 PowerPivot 数据刷新](power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)。  
  
 **本主题内容：**  
  
 [第 1 步：启用 Secure Store Service 并生成主密钥](#bkmk_services)  
  
 [步骤 2:关闭你不想要支持的凭据选项](#bkmk_creds)  
  
 [步骤 3:创建目标应用程序来存储数据刷新中使用的凭据](#bkmk_stored)  
  
 [步骤 4:为可缩放的数据刷新配置服务器](#bkmk_scale)  
  
 [步骤 5:安装用于导入 PowerPivot 数据的数据访问接口](#bkmk_installdp)  
  
 [步骤 6:授予创建计划和访问外部数据源的权限](#bkmk_accounts)  
  
 [步骤 7:启用数据刷新的工作簿升级](#bkmk_upgradewrkbk)  
  
 [步骤 8:验证数据刷新配置](#bkmk_verify)  
  
 [为数据刷新修改配置设置](#bkmk_config)  
  
 [重新计划 PowerPivot 数据刷新计时器作业](#configTimerJob)  
  
 [禁用数据刷新计时器作业](#bkmk_disableDR)  
  
 在您确保已配置了服务器环境和权限后，数据刷新可供使用。 若要使用数据刷新，SharePoint 用户需要针对 PowerPivot 工作簿创建一个计划，以便指定执行数据刷新的频率。 通常由将文件发布到 SharePoint 的工作簿所有者或作者来创建该计划。 该用户为其拥有的工作簿创建并管理数据刷新计划。 有关详细信息，请参阅[计划数据刷新&#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
##  <a name="bkmk_services"></a> 步骤 1:启用安全存储区服务并生成主密钥  
 要运行数据刷新作业以及连接到使用存储凭据的外部数据源，PowerPivot 数据刷新依赖 Secure Store Service 来提供所需的凭据。  
  
 如果您是使用“新服务器”选项安装 PowerPivot for SharePoint 的，则已为您配置 Secure Store Service。 对于所有其他安装方案，您必须创建和配置服务应用程序并为 Secure Store Service 生成主密钥。  
  
> [!NOTE]  
>  若要配置 Secure Store Service 或将 Secure Store Service 管理委托给其他用户，您必须是场管理员。 若要在启用设置后配置或修改设置，您必须是服务应用程序管理员。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  在服务应用程序功能区中的在中，单击**新建**。  
  
3.  选择**安全存储区服务**。  
  
4.  在中**创建安全存储应用程序**页上，输入应用程序的名称。  
  
5.  在中**数据库**，指定将承载此服务应用程序数据库的 SQL Server 实例。 默认值是承载场配置数据库的 SQL Server 数据库引擎实例。  
  
6.  在中**数据库名称**，输入服务应用程序数据库的名称。 默认值是 Secure_Store_Service_DB_\<guid >。 该默认名称对应于服务应用程序的默认名称。 如果您输入了唯一的服务应用程序名称，则遵循您的数据库名称的类似命名约定，以便可以一起管理它们。  
  
7.  在 **“数据库身份验证”** 中，默认值是 “Windows 身份验证”。 如果您选择“SQL 身份验证”，请参考 SharePoint 管理员指南中有关如何在场中使用该身份验证类型的说明。  
  
8.  在应用程序池选择**创建新应用程序池。** 请指定一个说明性名称，这将帮助其他服务器管理员标识使用此应用程序池的方式。  
  
9. 为应用程序池选择一个安全帐户。 指定要使用域用户帐户的托管帐户。  
  
10. 接受其他默认值，并单击**确定。** 服务应用程序将在场的服务应用程序列表中与其他托管服务显示在一起。  
  
11. 单击列表中的 Secure Store Service 应用程序。  
  
12. 在服务应用程序功能区中，单击**管理**。  
  
13. 在密钥管理，单击**生成新密钥**。  
  
14. 输入然后确认通行短语。 该通行短语将用于添加其他安全存储区共享服务应用程序。  
  
15. 单击“确定” 。  
  
 必须先启用存储区服务操作的日志记录审核功能（有助于故障排除），然后才能使用该功能。 有关如何启用日志记录的详细信息，请参阅[配置安全的存储区服务 (SharePoint 2010)](https://go.microsoft.com/fwlink/p/?LinkID=223294)。  
  
##  <a name="bkmk_creds"></a> 步骤 2:关闭不希望支持的凭据选项  
 PowerPivot 数据刷新在数据刷新计划中提供三个凭据选项。 工作簿所有者在计划数据刷新时会选择其中一个选项，由此决定用来运行数据刷新作业的帐户。 作为管理员，您可以决定可供计划所有者使用的凭据选项。  
  
 要运行数据刷新，必须至少提供一个选项。  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 选项 1**使用的数据刷新帐户由管理员配置**始终显示在计划定义页上，但仅适用于配置无人参与的数据刷新帐户。 有关如何创建帐户的详细信息，请参阅[配置 PowerPivot 无人参与的数据刷新帐户&#40;PowerPivot for SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。  
  
 选项 2，**使用以下 windows 凭据进行连接**始终显示在页上，但当您启用时才有效**允许用户输入自定义 Windows 凭据**服务中的选项应用程序配置页。 默认启用此选项，但您可以在使用此选项弊大于利的情况下禁用此选项（请参见下文）。  
  
 选项 3**使用在 Secure Store Service 中保存的凭据进行连接**始终显示在页上，但当计划所有者提供有效的目标应用程序时才有效。 管理员必须事先创建这些目标应用程序，然后向创建数据刷新计划的用户提供应用程序名称。 详细了解如何创建目标应用程序的数据刷新操作，请参阅[为 PowerPivot 数据刷新配置存储凭据&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
 **配置凭据选项 2，"使用以下 Windows 用户凭据连接"**  
  
 PowerPivot 服务应用程序包括一个凭据选项，该选项允许计划所有者任意输入 Windows 用户名和密码以便运行数据刷新作业。 这是计划定义页中的第二个凭据选项。  
  
 ![SSAS_PPS_ScheduleDataRefreshCreds](media/ssas-pps-scheduledatarefreshcreds.gif "SSAS_PPS_ScheduleDataRefreshCreds")  
  
 默认情况下启用此凭据选项。 启用此凭据选项后，PowerPivot 系统服务将在 Secure Store Service 中生成一个目标应用程序，用来存储计划所有者输入的用户名和密码。 使用此命名约定创建生成的目标应用程序：PowerPivotDataRefresh_\<guid >。 为每一组 Windows 凭据都创建一个目标应用程序。 如果由 PowerPivot 系统服务拥有的目标应用程序已存在，并且该应用程序存储着计划定义者输入的用户名和密码，则 PowerPivot 系统服务将使用该目标应用程序而不会另外新建。  
  
 此凭据选项的主要优点是简便易用。 由于系统为您创建了目标应用程序，所以几乎不需要执行进一步的工作。 此外，使用计划所有者（很可能就是工作簿创建者）的凭据运行数据刷新简化了之后的权限要求。 此用户很可能已经拥有针对目标数据库的权限。 当使用此人的 Windows 用户标识，任何数据连接指定的数据刷新运行时将会自动运行当前用户。  
  
 此选项的缺点是不易管理。 尽管目标应用程序是自动创建的，但它们不会随着帐户信息的更改自动删除或更新。 密码过期策略可能导致这些目标应用程序过期。 使用过期凭据的数据刷新作业将无法启动。 出现这种情况时，计划所有者需要通过提供数据刷新计划中的当前用户名和密码值来更新自己的凭据。 此时将创建一个新的目标应用程序。 之后随着用户不断添加和修改他们数据刷新计划中的凭据信息，您会发现自己的系统上存在大量自动生成的目标应用程序。  
  
 当前无法确定哪些目标应用程序是活动的，哪些不活动；也无法通过特定目标应用程序回溯到使用它的数据刷新计划。 通常，您应该不对这些目标应用程序执行任何操作，因为删除它们可能会破坏现有的数据刷新计划。 删除仍在使用的目标应用程序将导致数据刷新失败并显示消息，"目标应用程序找不到"，使其不显示该工作簿的数据刷新历史记录页。  
  
 如果选择禁用此凭据选项，则可以安全地删除为 PowerPivot 数据刷新生成的所有目标应用程序。  
  
 **禁用数据刷新计划中的任意 Windows 凭据的使用**  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击 PowerPivot 服务应用程序名称。 PowerPivot 管理面板将出现。  
  
3.  在操作中，单击**配置服务应用程序设置**以打开 PowerPivot 服务应用程序设置页  
  
4.  在数据刷新部分中，清除**允许用户输入自定义 Windows 凭据**复选框。  
  
     ![SSAS_PowerPivotDatarefreshOptions_AllowUser](media/ssas-powerpivotdatarefreshoptions-allowuser.gif "SSAS_PowerPivotDatarefreshOptions_AllowUser")  
  
##  <a name="bkmk_stored"></a> 步骤 3:创建用于存储数据刷新中所使用的凭据的目标应用程序  
 一旦配置了 Secure Store Service，SharePoint 管理员就可以创建目标应用程序以使存储的凭据可用于数据刷新，包括无人参与的 PowerPivot 数据刷新帐户或者用于运行数据刷新作业或连接到外部数据源的任何其他帐户。  
  
 回想上一部分中所述的内容，您需要创建目标应用程序才能使特定凭据选项可用。 具体而言，您必须为 PowerPivot 无人参与的数据刷新帐户以及要在数据刷新操作中使用的其他任何存储凭据创建目标应用程序。  
  
 有关如何创建包含存储的凭据的目标应用程序的详细信息，请参阅[配置 PowerPivot 无人参与的数据刷新帐户&#40;PowerPivot for SharePoint&#41; ](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)并[为 PowerPivot 数据刷新配置存储的凭据&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
##  <a name="bkmk_scale"></a> 步骤 4:配置服务器用于可扩展的数据刷新  
 默认情况下，每个 PowerPivot for SharePoint 安装都支持按需查询和计划的数据刷新。  
  
 对于每个安装，您都可以指定 Analysis Services 服务器实例是同时支持查询和计划的数据刷新，还是专用于特定类型的操作。 如果场中安装有多个 PowerPivot for SharePoint，在您发现作业出现延迟或失败的情况下，可以考虑将某台服务器专用于数据刷新操作。  
  
 此外，如果基础硬件支持，则可以增加可同时运行的数据刷新作业的数目。 默认情况下，将根据系统内存来计算可同时运行的作业数目；但如果 CPU 有额外处理能力来支持负载，则可以增加该数目。  
  
 有关详细信息，请参阅[配置专用数据刷新或 Query-Only 处理&#40;PowerPivot for SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)。  
  
##  <a name="bkmk_installdp"></a> 步骤 5:安装用于导入 PowerPivot 数据的数据访问接口  
 数据刷新操作基本上是对检索原始数据的导入操作的重复。 这意味着用于在 PowerPivot 客户端应用程序中导入数据的数据访问接口也必须安装在 PowerPivot 服务器上。  
  
 您必须是本地管理员才能在 Windows 服务器上安装数据访问接口。 如果您安装其他驱动程序，请确保在 SharePoint 场中安装了 PowerPivot for SharePoint 的每台计算机上安装这些驱动程序。 如果您在场中具有多个 PowerPivot 服务器，则必须在每个服务器上都安装这些访问接口。  
  
 请记住，SharePoint 服务器是 64 位应用程序。 请务必安装您准备用于支持数据刷新操作的数据访问接口的 64 位版本。  
  
##  <a name="bkmk_accounts"></a> 步骤 6:授予创建计划和访问外部数据源所需的权限  
 工作簿所有者或作者必须具有 **“参与讨论”** 权限才能计划针对工作簿的数据刷新。 给定此权限级别，他或她可以打开和编辑工作簿的数据刷新配置页来指定的凭据和计划用于刷新数据的信息。  
  
 除 SharePoint 权限之外，还必须检查针对外部数据源的数据库权限，以确保数据刷新过程中使用的帐户对该数据具有足够的访问权限。 确定权限要求时需要您仔细评估，因为您需要授予的权限将根据工作簿中的连接字符串和运行数据刷新作业所用的用户身份而有所不同。  
  
 **PowerPivot 工作簿中现有的连接字符串为何对 PowerPivot 数据刷新操作很重要**  
  
 运行数据刷新时，服务器会使用最初导入数据时创建的连接字符串向外部数据源发送连接请求。 刷新数据期间，需要再次使用该连接字符串中指定的服务器位置、数据库名称和身份验证参数来访问相同的数据源。 不能为了刷新数据而修改连接字符串及其整体构造。 在数据刷新过程中只能按原样再次使用连接字符串。 在某些情况下，如果您使用 Windows 身份验证之外的方式连接数据源，则可以覆盖该连接字符串中的用户名和密码。 本主题下文将对此进行详细解释。  
  
 对于多数工作簿，针对连接的默认身份验证选项是使用可信连接或 Windows 集成安全性，这导致连接字符串中包含 `SSPI=IntegratedSecurity` 或 `SSPI=TrustedConnection`。 在数据刷新过程中使用此连接字符串时，用来运行数据刷新作业的帐户将成为当前用户。 因此，此帐户需要对通过可信连接访问的所有外部数据源都具有读取权限。  
  
 **您是否启用 PowerPivot 无人参与的数据刷新帐户？**  
  
 如果是，则应授予该帐户针对数据刷新期间所访问数据源的读取权限。 刷新此帐户为何需要读取权限，是因为使用的默认身份验证选项的工作簿中的无人参与的帐户将当前用户期间数据的原因。 除非计划所有者覆盖连接字符串中的凭据，否则此帐户将需要对组织中频繁使用的所有数据源都拥有读取权限。  
  
 **是否使用凭据选项 2： 允许计划所有者输入 Windows 用户名和密码？**  
  
 通常，创建 PowerPivot 工作簿的用户已经具有足够的权限，因为该用户最初已经导入了数据。 如果这些用户随后将数据刷新配置为采用他们自己的 Windows 用户身份运行，则将在数据刷新期间使用他们的 Windows 用户帐户（已经具有数据库权限）来检索数据。 已有的权限应该就足够了。  
  
 **是否使用凭据选项 3： 使用 Secure Store Service 目标应用程序提供用于运行数据刷新作业的用户标识？**  
  
 用于运行数据刷新作业的任何帐户都需要读取权限，其原因与为 PowerPivot 无人参与的数据刷新帐户描述的原因相同。  
  
 **如何检查连接字符串以确定您是否能够覆盖数据刷新过程中使用的凭据**  
  
 如上所述，如果连接使用 Windows 身份验证之外的方式（例如 SQL Server 身份验证），则您可以在数据刷新作业级别提供不同的用户名和密码。 使用用户 ID 和密码参数向连接字符串传递非 Windows 凭据。 如果工作簿包含具有这些参数的连接字符串，您可以选择指定不同的用户名和密码，用来刷新来自该数据源的数据。  
  
 以下各步解释如何确定您的连接字符串是否接受用户名和密码覆盖。  
  
1.  在 Excel 中打开工作簿。  
  
2.  打开 PowerPivot 窗口（在 Excel 中的 PowerPivot 功能区上，单击“PowerPivot”窗口）。  
  
3.  单击**设计**。  
  
4.  单击**现有连接**。  
  
     下会列出所有工作簿中使用的连接**PowerPivot 数据连接**。  
  
5.  选择连接，然后单击**编辑**，然后单击**高级**。 连接字符串位于该页底部。  
  
 如果您看到**Integrated Security = SSPI**在连接字符串中，您不能覆盖连接字符串中的凭据。 将始终使用当前用户身份连接， 忽略您提供的所有凭据。  
  
 如果您看到**Persist Security Info = False，Password =\* \* \* \* \* \* \* \* \* \* \*，UserID =\<userlogin >**，则必须接受凭据覆盖连接字符串。 连接字符串中显示的凭据（如 UserID 和密码）并不是 Windows 凭据，而是对目标数据源有效的数据库登录名或其他登录帐户。  
  
 **如何重写连接字符串中的凭据**  
  
 通过在数据刷新计划中指定数据源凭据来覆盖凭据。 作为管理员，您可以提供 Secure Store Service 中的目标应用程序来映射用来访问外部数据的凭据。 然后，计划所有者可以在数据刷新计划中输入其定义的目标应用程序 ID。 有关创建此目标应用程序的详细信息，请参阅[为 PowerPivot 数据刷新配置存储凭据&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)。  
  
 或者，计划所有者可以键入在数据刷新期间用于连接数据源的一组凭据。 下图显示了计划定义页中的这一数据源选项。  
  
 ![SSAS_PowerPivotKJ_DataRefreshDSOptions](media/ssas-powerpivotkj-datarefreshdsoptions.gif "SSAS_PowerPivotKJ_DataRefreshDSOptions")  
  
 **标识数据访问要求**  
  
 如上所述，用于运行数据刷新和连接外部数据源的帐户经常是同一个帐户。 因此，用于访问外部数据源的帐户由数据刷新计划页这一部分中设置的选项来决定。 该帐户可能是 PowerPivot 无人参与的数据刷新帐户、个人用户的 Windows 帐户，或是存储在预定义目标应用程序中的帐户。  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 如果运行数据刷新所用的帐户不同于导入数据所用的帐户（例如，通过凭据选项 1 设置的 PowerPivot 无人参与数据刷新帐户或是通过凭据选项 3 设置的其他任何一组存储凭据），您将需要为该帐户创建新的数据库登录名，并授予其针对外部数据源的读取权限。  
  
 在了解哪些帐户需要数据访问权限后，您可以开始检查在 PowerPivot 工作簿中最常用的数据源的权限。 从频繁使用的任何数据仓库或报告数据库开始，但同时也要询问您最活跃的 PowerPivot 用户，了解他们所用的数据源。 掌握数据源列表后，则可以开始检查各个数据源，确保权限设置正确。  
  
##  <a name="bkmk_upgradewrkbk"></a> 步骤 7:为数据刷新启用工作簿升级  
 默认情况下，在 PowerPivot for SharePoint 的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 版本上，无法将使用 PowerPivot for Excel 的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本创建的工作簿配置用于计划数据刷新。 如果在 SharePoint 环境中同时托管 PowerPivot 工作簿的较新版本和较旧版本，则必须先升级所有 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 工作簿，然后才能安排在服务器上对这些工作簿执行自动数据刷新。  
  
##  <a name="bkmk_verify"></a> 步骤 8:验证数据刷新配置  
 若要验证数据刷新，您必须具有发布到 SharePoint 站点的 PowerPivot 工作簿。 您必须具有针对该工作簿的“参与讨论”权限，以及访问数据刷新计划中包括的任何数据源所需的权限。  
  
 在创建计划时，选择**也尽快刷新**复选框以立即运行数据刷新。 随后可以检查该工作簿的数据刷新历史记录页，验证刷新是否成功。 请记住“PowerPivot 数据刷新计时器作业”每分钟运行一次。 所以至少也需要同样长的时间才能得到关于数据刷新成功与否的确认。  
  
 务必尝试您计划支持的所有凭据选项。 例如，如果配置了 PowerPivot 无人参与的数据刷新帐户，请验证使用该选项是否成功执行了数据刷新。 有关计划和查看状态信息的详细信息，请参阅[计划数据刷新&#40;PowerPivot for SharePoint&#41; ](schedule-a-data-refresh-powerpivot-for-sharepoint.md)并[查看数据刷新历史记录&#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 如果数据刷新失败，请参阅[解决 PowerPivot 数据刷新](https://go.microsoft.com/fwlink/?LinkID=223279)可能的解决方案的 TechNet wiki 上的页。  
  
##  <a name="bkmk_config"></a> 为数据刷新修改配置设置  
 每个 PowerPivot 服务应用程序都具有影响数据刷新操作的配置设置。 本节介绍如何修改这些设置。  
  
###  <a name="procIntervals"></a> 设置工作时间来确定非工作时间处理  
 计划数据刷新操作的 SharePoint 用户可以指定“在工作时间后”的最早开始时间。 如果用户要检索在工作日内累计的业务交易数据，则这可能会很有用。 作为场管理员，您可以为您的组织指定最恰当地定义工作日的小时数范围。 如果将工作日定义为从 04:00 到 20:00，则基于开始时间为“在工作时间后”的数据刷新处理将在 20:01 开始。  
  
 在非工作时间内运行的数据刷新请求将按照接收该请求的顺序添加到队列中。 在服务器资源变得可用时，将处理各个请求。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击 PowerPivot 服务应用程序名称。 PowerPivot 管理面板将出现。  
  
3.  在操作中，单击**配置服务应用程序设置**以打开 PowerPivot 服务应用程序设置页  
  
4.  在“数据刷新”部分的“工作时间”中输入开始时间和结束时间，以定义工作时间后的处理期间。  
  
     如果您不希望定义非工作时间处理期间，可以在“开始时间”和“结束时间”中输入同样的值（例如，两个时间均为 12:00）。 但应注意，SharePoint 站点上的计划定义页仍将“在工作时间后”作为一个选项。 在未定义非工作时间处理范围的场中选择该选项的用户将最终获得数据刷新错误，因为处理作业无法开始。  
  
5.  单击“确定” 。  
  
###  <a name="usagehist"></a> 限制数据刷新历史记录的保留期  
 数据刷新历史记录用于详细记录数据刷新操作随着时间推移生成的成功和失败消息。 通过场中的使用情况数据收集系统可以收集和管理历史记录信息。 因此，您对使用情况数据历史记录设置的限制也适用于数据刷新历史记录。 因为使用情况活动报表将来自整个 PowerPivot 系统的数据收集在一起，所以，单个历史记录设置用于同时为数据刷新历史记录和所收集和存储的所有其他使用情况数据控制数据保留事宜。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击 PowerPivot 服务应用程序名称。 PowerPivot 管理面板将出现。  
  
3.  在操作中，单击**配置服务应用程序设置**以打开 PowerPivot 服务应用程序设置页  
  
4.  在“使用情况数据收集”部分的“使用情况数据历史记录”中，键入您希望为每个工作簿保留数据刷新活动记录的天数。  
  
     默认值为 365 天。 最小值为 1 天，最大值为 5000 天。 0 指定保留期不受限制；数据始终不会被删除。 请注意，不存在用于关闭历史记录的设置。  
  
5.  单击“确定” 。  
  
 当 SharePoint 用户在具有数据刷新历史记录的工作簿上选择“管理数据刷新”选项时，这些用户将可以使用历史记录信息。 场管理员用来管理 PowerPivot 服务操作的 PowerPivot 管理面板中也使用了此信息。 有关详细信息，请参阅[查看数据刷新历史记录&#40;PowerPivot for SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)。  
  
 历史记录数据的长期物理存储位于 PowerPivot 服务应用程序的 PowerPivot 服务应用程序数据库中。 有关如何收集和存储使用情况数据的详细信息，请参阅[PowerPivot 使用情况数据收集](power-pivot-sharepoint/power-pivot-usage-data-collection.md)。  
  
##  <a name="configTimerJob"></a> 重新计划 PowerPivot 数据刷新计时器作业  
 计划的数据刷新由 PowerPivot 数据刷新计时器作业触发，此作业以一分钟为间隔扫描 PowerPivot 服务应用程序数据库中的计划信息。 当数据刷新按计划开始时，计时器作业将请求添加到可用 PowerPivot 服务器上的处理队列中。  
  
 您可以增加扫描之间的时间长度以作为一种性能优化方法。 还可以在排除问题时禁用此计时器作业，以暂时停止数据刷新操作。  
  
 默认设置为一分钟，这是您可以指定的最小值。 这是建议采用的值，因为它可以为在一天中的任意时间运行的计划提供可预测性最好的结果。 例如，如果用户计划在 4:15 PM 刷新数据，而计时器作业每分钟扫描一次计划，则将在 4:15 检测到计划的数据刷新请求，并在 4:15 后的几分钟内进行处理。  
  
 如果您加大该扫描时间间隔以便扫描极少运行（例如，每天午夜一次），则计划在该时间间隔中运行的所有数据刷新操作将一次全都添加到处理队列中，这可能导致大量占用服务器资源并且导致其他应用缺乏系统资源。 根据计划的刷新的数目，数据刷新操作的处理队列可能累积到并非所有作业都能完成的程度。 当位于队列末尾的数据刷新请求进入下一个处理间隔时，可能导致这些请求被丢弃。  
  
 如果您的硬件支持，您可以通过指定附加处理器来并行运行多个数据刷新作业，缓解这一问题。 有关详细信息，请参阅[配置专用数据刷新或 Query-Only 处理&#40;PowerPivot for SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)。 有关如何发现、 添加到队列和处理数据刷新请求的详细信息，请参阅[PowerPivot 数据刷新](power-pivot-sharepoint/power-pivot-data-refresh.md)。  
  
1.  在管理中心中，单击 **“监视”**。  
  
2.  单击 **“检查作业定义”**。  
  
3.  选择**PowerPivot 数据刷新计时器作业**。  
  
4.  修改计划频率，以更改计时器作业扫描数据刷新计划信息的频率。  
  
##  <a name="bkmk_disableDR"></a> 禁用数据刷新计时器作业  
 PowerPivot 数据刷新计时器作业是场级别计时器作业，可以对场中的所有 PowerPivot 服务器实例启用或禁用此作业。 它与特定的 Web 应用程序或 PowerPivot 服务应用程序无关。 您无法在某些服务器上禁用它，以强制对场中的其他服务器进行数据刷新处理。  
  
 如果您禁用 PowerPivot 数据刷新计时器作业，则将处理已位于队列中的请求，但在重新启用该作业前，不会添加新请求。 系统将不处理计划在过去发生的请求。  
  
 禁用计时器作业不会影响应用程序页中的功能可用性。 无法删除或隐藏 Web 应用程序中的数据刷新功能。 具有“参与讨论”权限或更高权限的用户仍可创建新的数据刷新操作计划，即使计时器作业已被永久禁用也不例外。  
  
## <a name="see-also"></a>请参阅  
 [计划数据刷新&#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [配置专用的数据刷新或仅限查询的处理&#40;PowerPivot for SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)   
 [配置 PowerPivot 无人参与的数据刷新帐户&#40;PowerPivot for SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [为 PowerPivot 数据刷新配置存储的凭据&#40;PowerPivot for SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
