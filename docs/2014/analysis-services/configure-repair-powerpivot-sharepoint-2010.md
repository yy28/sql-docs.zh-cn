---
title: 配置或修复 PowerPivot for SharePoint 2010 （PowerPivot 配置工具） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d61f49c5-efaa-4455-98f2-8c293fa50046
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d89de37de81311b1f4a884eeaf434e8247da633
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174466"
---
# <a name="configure-or-repair-powerpivot-for-sharepoint-2010-powerpivot-configuration-tool"></a>配置或修复 PowerPivot for SharePoint 2010（PowerPivot 配置工具）
  要配置或修复 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerPivot for SharePoint 2010 的安装，请使用 PowerPivot 配置工具。 该配置工具开始是扫描系统，然后返回完成或修复安装所需的操作列表。 
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 安装向导将安装用于 SharePoint 2010 的 PowerPivot 配置工具以及用于 SharePoint 2013 的 PowerPivot 配置工具。 本主题介绍用于 SharePoint 2010 的 PowerPivot 配置工具。 有关 SharePoint 2010 的详细信息，请参阅[PowerPivot for SharePoint 2013 &#40;PowerPivot 配置工具&#41;中配置或修复](power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md)。

 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010

 

##  <a name="bkmk_before"></a>开始之前
 PowerPivot for SharePoint 2010 配置工具扫描程序文件、注册表设置和可用端口。 若要充分利用该工具，请先查看以下内容。

-   运行 [PowerPivot Configuration Tools](power-pivot-sharepoint/power-pivot-configuration-tools.md)的一般要求。

-   PowerPivot for SharePoint 2010 需要配置为使用经典模式身份验证的 Web 应用程序。 如果 PowerPivot for SharePoint 2010 配置工具为您创建了应用程序，则该应用程序将配置为经典模式。

-   端口 80 必须可用于所选任务之一，它要求配置工具创建并配置 Web 应用程序。

##  <a name="bkmk_using"></a>使用 PowerPivot 配置工具
 该工具的第一页提供了用于配置 SharePoint 场的输入值汇总。 除了您提供的输入值之外，将使用默认值来配置系统。 默认名称用于服务应用程序、服务应用程序数据库和服务应用程序属性。

> [!TIP]
>  如果 PowerPivot 配置工具扫描计算机并在左窗格中返回一个空白任务列表，则无需配置任何功能和设置。 若要修改 SharePoint 或 PowerPivot 配置，请使用 Windows PowerShell 或 SharePoint 管理中心的管理页。 有关详细信息，请参阅[在管理中心中管理和配置 PowerPivot 服务器](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)。

 服务帐户的值将用于多个服务。 例如，PowerPivot 配置工具使用第一页上的默认帐户来设置所有应用程序池标识。 可以通过在管理中心中修改服务应用程序属性在以后更改这些帐户。

-   在 PowerPivot for SharePoint 2010 配置工具中，该规则的例外情况是 Analysis Services 服务帐户。 此帐户在安装过程中指定，并且您在 **“在本地服务器上注册 SQL Server Analysis Services (PowerPivot)”** 操作中为此帐户键入密码。 该汇总页不包含用于此密码的字段，因此，请确保在针对该操作的页面中输入此密码。

 该工具提供了一个选项卡式界面，其中包括参数输入、Windows PowerShell 脚本和状态消息。

 PowerPivot 配置工具使用 Windows PowerShell 来配置服务器。 您可以单击 **“脚本”** 选项卡以查看 Windows PowerShell 脚本。

 ![“配置工具”用户界面](media/ssas-pctui.gif "“配置工具”用户界面")

##  <a name="bkmk_steps"></a>配置步骤
 只有在本地服务器上安装了 PowerPivot for SharePoint 2010 后，才会显示指向该配置工具的链接。

1.  在 **“开始”** 菜单中，指向 **“所有程序”**，依次单击 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]、 **“配置工具”** 和 **“PowerPivot 配置工具”**。

2.  单击 **“配置或修复 PowerPivot for SharePoint”**。

3.  将窗口放大为实际大小。 您应该在该窗口的底部看到一个菜单栏，其中包含 **“验证”**、 **“运行”** 和 **“退出”** 命令。

4.  **默认帐户：** 在 "参数" 选项卡上，键入 "**默认帐户用户名**" 的域用户帐户。 此帐户用于设置重要服务，包括 PowerPivot 服务应用程序池。 不要指定 Network Service 或 Local System 之类的内置帐户。 该工具将阻止指定内置帐户的配置。

     **通行短语：** 键入通行短语。 对于新的 SharePoint 场，在向该 SharePoint 场中添加新的服务器或应用程序时，需要使用该通行短语。 对于已存在的场，输入允许您向该场添加服务器应用程序的通行短语。

5.  **端口：**（可选）键入用于连接到管理中心 web 应用程序的端口号，或使用提供的随机生成的编号。 该配置工具将首先检查该端口号是否可用，然后将其作为选项提供。

6.  单击 **“在本地服务器上注册 SQL Server Analysis Services (PowerPivot)”**。

     输入 Analysis Services 服务帐户的密码。

7.  或者，查看用于完成各操作的剩余输入值。 有关每个输入值的详细信息，请参阅本主题中的 [用于配置服务器的输入值](#bkmk_input) 。

8.  您还可以选择删除不想处理的任何操作。 例如，如果您想要在以后配置 Secure Store Service，则单击 **“配置 Secure Store Service”**，然后清除 **“在任务列表中包括此操作”** 复选框。

9. 单击 **“验证”** 以便检查该工具是否有足够的信息来处理列表中的操作。

    > [!NOTE]
    >  如果您收到了场配置错误，则原因可能是未安装 SharePoint 2010 Server SP1。

10. 单击 **“运行”** 来处理该任务列表中的所有操作。 
  **“运行”** 按钮将在您验证操作之后启用。 如果 **“运行”** 未启用，请首先单击 **“验证”** 。

11. [验证 PowerPivot for SharePoint 安装](instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)。

##  <a name="bkmk_input"></a>用于配置服务器的输入值
 PowerPivot 配置工具组合使用您键入的输入值以及它检测到或自动使用的默认值。

 配置工具中列出的操作列表取决于 SharePoint 场的当前配置。 例如，如果已配置 SharePoint 场，则工具中将不会列出任何操作。 您可以随时运行工具以便配置、修复或检测到配置错误。 如果所需服务（例如 Excel Services 或 Secure Store Service）未在场中运行，则该工具将检测到缺失的服务并且提供用于启用这些服务的选项。 如果无需执行任何操作，则任务列表将是空的。

 下表说明了用于配置服务器的值。

|页|输入值|源|说明|
|----------|-----------------|------------|-----------------|
|**“配置或修复 PowerPivot for SharePoint”**|默认帐户|当前用户|默认帐户是用于在场中设置共享服务的域 Windows 用户帐户。 该帐户用于设置 PowerPivot 服务应用程序、Secure Store Service、Excel Services、Web 应用程序池标识、网站集管理员和 PowerPivot 无人参与的数据刷新帐户。<br /><br /> 默认情况下，该工具将输入当前用户的域帐户。 除非您是为评估目的配置服务器，否则，应该使用其他域用户帐户替换该默认帐户。<br /><br /> 您还可以在以后使用管理中心来更改服务标识。<br /><br /> 或者，在 PowerPivot 配置工具中，您可为以下项指定专用的帐户：<br /><br /> Web 应用程序，使用 **“创建默认的 Web 应用程序”** 页（假定该工具正在为场创建 Web 应用程序）。<br /><br /> PowerPivot 无人参与的数据刷新帐户，使用此工具中的 **“为数据刷新创建无人参与的帐户”** 页。|
||数据库服务器|本地 PowerPivot 命名实例（如果可用）|如果数据库引擎实例作为 PowerPivot 命名实例安装，则该工具将使用此实例填充数据库服务器字段。 如果您没有安装数据库引擎，此字段将为空。 您必须提供一个实例。 该实例可以是支持 SharePoint 场的任何 SQL Server 版本或发行版。|
||通行短语|用户输入|如果您在创建新的场，则您输入的通行短语将是该场的通行短语。 如果您在向现有场添加 PowerPivot for SharePoint，则必须提供在创建时为该场定义的通行短语。|
||SharePoint 管理中心端口|默认值（如果需要）|如果未配置场，该工具将提供用于创建场的选项，包括指向管理中心的 HTTP 端点。 它默认为一个未使用的随机生成的端口号。|
|**配置新场**|数据库服务器<br /><br /> 场帐户<br /><br /> 通行短语<br /><br /> SharePoint 管理中心端口|默认值（如果需要）|这些设置默认为在主页上输入的设置。|
|**配置本地服务实例**|Analysis Services 服务帐户密码|用户输入|您必须在 **“在本地服务器上注册 SQL Server Analysis Services (PowerPivot)”** 页中键入 Analysis Services 服务帐户的密码。<br /><br /> 该服务帐户是在安装过程中指定的。 您现在必须将密码作为输入键入以便向 SharePoint 注册本地服务实例。|
|**创建 PowerPivot 服务应用程序**|PowerPivot 服务应用程序名称|默认|默认名称为默认的 PowerPivot 服务应用程序。 您可以在该工具中替换为不同的值。|
||PowerPivot 服务应用程序数据库服务器|默认|承载 PowerPivot 服务应用程序数据库的数据库服务器。 默认服务器名称与用于该场的数据库服务器相同。 您可以在该工具中替换为不同的值。|
||PowerPivot 服务应用程序数据库名称|默认|默认数据库名称基于服务应用程序名称，后跟 GUID 以便确保名称唯一。 您可以在该工具中替换为不同的值。|
||升级工作簿以启用数据刷新|用户输入|数据刷新失败，并且 SQL Server 2008 R2 PowerPivot 工作簿不支持此功能。 
  **“升级工作簿以启用数据刷新”** 选项将工作簿升级到 SQL Server 2012 PowerPivot 版本。|
|**创建默认的 Web 应用程序**|Web 应用程序名称|默认值（如果需要）|如果不存在任何 Web 应用程序，该工具将创建一个。 Web 应用程序配置为使用经典模式身份验证，并侦听 **端口 80**。 最大文件上载大小设为 2047 MB，这是 SharePoint 所允许的最大值。 较大的文件上载大小用于容纳大型 PowerPivot 文件。|
||代码|默认值（如果需要）|该工具将基于服务器名称创建一个 URL，并且使用与 SharePoint 相同的文件命名约定。|
||Web 应用程序池|默认值（如果需要）|该工具在 IIS 中创建默认应用程序池。|
||Web 应用程序池帐户和密码|默认值（如果需要）|该应用程序池帐户基于默认帐户，但您可以在该工具中替换它。|
||Web 应用程序数据库服务器|默认值（如果需要）|将预先选择默认数据库实例以便存储应用程序数据库，但您可以在该工具中指定不同的 SQL Server 实例。|
||Web 应用程序数据库名称|默认值（如果需要）|该数据库名称基于 SharePoint 的文件命名约定，但您可以选择其他名称。|
|**部署 Web 应用程序解决方案**|代码|默认值（如果需要）|默认 URL 来自默认的 Web 应用程序。|
||最大文件大小(MB)|默认值（如果需要）|默认设置为 2047。 SharePoint 文档库也有一个最大大小，且 PowerPivot 设置不应超过此文档库设置。 有关详细信息，请参阅[&#40;PowerPivot for SharePoint&#41;配置最大文件上传大小](power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。|
|**创建网站集**|站点管理员|默认值（如果需要）|此工具将使用默认帐户。 您可以在 **“创建网站集”** 页中覆盖默认帐户。|
||联系人电子邮件|默认值（如果需要）|如果在服务器上配置了 Microsoft Outlook，则该工具将使用当前用户的电子邮件地址。 否则，将使用占位符值。|
||站点 URL|默认值（如果需要）|该工具将创建网站 URL，并且使用与 SharePoint 相同的 URL 命名约定。|
||网站标题|默认值（如果需要）|此工具将添加 **“PowerPivot 网站”** 作为默认标题。|
|**激活网站集中的 PowerPivot 功能**|站点 URL||激活 PowerPivot 功能的网站集的 URL。|
||为此网站启用高级功能||启用 SharePoint 网站功能 "PremiumSite"。|
|**创建 Secure Store Service 应用程序**|服务应用程序名称||键入 Secure Store Service 应用程序的名称。|
||数据库服务器||键入用于 Secure Store Service 应用程序的数据库服务器的名称。|
|**创建 Secure Store Service 应用程序代理**|服务应用程序名称||键入 Secure Store Service 应用程序的名称。|
||服务应用程序代理||键入 Secure Store Service 应用程序代理的名称。  该名称将出现在默认连接组中，该连接组将应用程序与 SharePoint 内容 Web 应用程序相关联。|
|**更新 Secure Store Service 主密钥**|服务应用程序代理||键入 Secure Store Service 应用程序代理的名称|
||通行短语||主密钥用于数据加密。 默认情况下，用于生成密钥的通行短语是用来在场中设置新服务的相同通行短语。 您可以将默认通行短语替换为唯一通行短语。|
|**为 Datarefresh 创建无人参与帐户**|目标应用程序 ID||应用程序 ID 可以为说明文本。|
||目标应用程序的友好名称|||
||无人参与的帐户用户名和密码||键入由目标应用程序用来运行无人参与的数据刷新操作的 Windows 用户帐户的凭据。|
||站点 URL||键入与目标应用程序关联的网站集的网站 URL。 若要与其他网站集关联，请使用 SharePoint 管理中心。|
|**创建 Excel Services 服务应用程序**|服务应用程序名称||键入服务应用程序名称。 将在 SharePoint 场的数据库服务器上创建一个具有相同名称的服务应用程序数据库。|
|**将 MSOLAP.5 作为受信任提供程序添加**|服务应用程序名称||SharePoint 2010 中的 Excel Services 使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] OLE DB 访问接口连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据。 此步骤会将随 PowerPivot for SharePoint 安装的 OLE DB 访问接口版本作为可信的数据访问接口添加到 Excel Services。|
||PowerPivot 服务器名称|||
|||||

 如果该 PowerPivot 配置工具创建场，它将使用与 SharePoint 相同的文件命名约定在数据库服务器上创建所需的数据库。 不能更改场数据库名称。

 如果该工具创建网站集，它将在数据库服务器上创建内容数据库，并且使用与 SharePoint 相同的文件命名约定。 不能更改内容数据库名称。

##  <a name="bkmk_nextsteps"></a>后续步骤
 完成服务器安装后，您应该执行若干安装后任务：

-   将 SharePoint 权限授予各个用户和组。 此任务是启用对站点和内容的访问所必需的。

-   更改服务应用程序池标识符以便在其他帐户下运行。 为服务和应用程序指定不同的标识是实现安全部署的 SharePoint 最佳实践建议。

-   在 Excel Services 中创建其他可信站点，以便您可以改变最适合进行 PowerPivot 数据访问的权限和配置设置。

-   安装 ADO.NET Data Services 3.5 SP1 以便启用从 SharePoint 列表的数据馈送导出。

-   安装常用的数据访问接口来启用服务器端数据刷新。

-   将 PowerPivot 创作工具下载到您的工作站计算机，以便创建 PowerPivot 工作簿，然后将其发布到 SharePoint。 安装该工具并发布 PowerPivot 工作簿验证了您刚安装的服务器组件的互操作性，从而完成了安装周期。

### <a name="grant-sharepoint-permissions-to-workbook-users"></a>向工作簿用户授予 SharePoint 权限
 用户将首先需要 SharePoint 权限，然后才能发布或查看工作簿。 请确保对需要查看已发布工作簿的用户授予 **“查看”** 权限，对发布或管理工作簿的用户授予 **“参与讨论”** 权限。 您必须是网站集管理员才能授予权限。

1.  在网站中，单击 **“网站操作”**。

2.  单击 **“网站权限”**。

3.  根据需要创建用户组，例如可以创建一个具有 **“参与”** 权限的用户组，以及一个仅具有 **“查看”** 权限的用户组。

4.  输入分属各个组成员的 Windows 域用户或组帐户。 与前面一样，如果将应用程序配置为采用经典身份验证，则不要使用电子邮件地址或分发组。

### <a name="install-adonet-data-services-35-sp1"></a>安装 ADO.NET Data Services 3.5 SP1
 ADO.NET Data Services 是 SharePoint 列表的数据馈送导出所必需的。 SharePoint 2010 在 PrerequisiteInstaller 程序中不包括此组件，因此您必须手动安装它。

1.  转到针对 SharePoint 2010 的硬件和软件要求文档 [确定硬件和软件要求 (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)

2.  在“安装必备软件”中，找到用于与您正在使用的操作系统相对应的 ADO.NET Data Services 3.5 的链接。

3.  单击该链接并且运行安装该服务的安装程序。

### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>安装数据刷新中使用的数据访问接口和检查用户权限
 服务器端数据刷新使用户可以在无人参与模式下将更新后的数据重新导入到其工作簿中。 为了成功执行数据刷新，服务器必须具有用于最初导入数据的同一个数据访问接口。 此外，运行数据刷新的用户帐户通常需要对外部数据源具有读取权限。 请务必检查启用和配置数据刷新的要求，以确保获得成功结果。 有关详细信息，请参阅[通过 SharePoint 2010 进行 PowerPivot 数据刷新](powerpivot-data-refresh-with-sharepoint-2010.md)。

### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>更改 SharePoint 中的应用程序池和服务标识
 PowerPivot 配置工具将场功能、应用程序和服务设置为在单个帐户下运行。 这简化了安装，但会导致部署无法满足 SharePoint 场的安全要求。 若要创建更可靠的部署，请在完成安装后，将应用程序池和服务标识更改为基于不同的帐户运行。 有关详细信息，请参阅[配置 PowerPivot 服务帐户](power-pivot-sharepoint/configure-power-pivot-service-accounts.md)。

### <a name="create-additional-trusted-sites-in-excel-services"></a>在 Excel Services 中创建其他可信站点
 您可以在 Excel Services 中添加可信站点，以便在提供 Excel 工作簿和 PowerPivot 数据的站点上改变权限和配置设置。 有关详细信息，请参阅 [Create a trusted location for PowerPivot sites in Central Administration](power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。

### <a name="add-servers-or-applications"></a>添加服务器或应用程序
 一段时间后，如果您确定需要附加的数据存储和处理能力，则可以将第二个 PowerPivot for SharePoint 服务器实例添加到场中。 有关说明，请参阅[部署清单：通过将 PowerPivot 服务器添加到 SharePoint 2010 场进行扩展](../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。

## <a name="additional-resources"></a>其他资源
 ![SharePoint 设置](media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")https://connect.microsoft.com/SQLServer/Feedback)[通过 Microsoft SQL Server Connect （）提交反馈和联系信息](https://connect.microsoft.com/SQLServer/Feedback)。

## <a name="see-also"></a>另请参阅
 [Powerpivot 配置工具](power-pivot-sharepoint/power-pivot-configuration-tools.md)[管理中心中的 powerpivot 服务器管理和配置](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)


