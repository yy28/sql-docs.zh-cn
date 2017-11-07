---
title: "配置或修复 Power Pivot for SharePoint 2013 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 616877e3-464a-4c97-bc74-1fa6f4faa756
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2920b6663bce5bcd82f16f4fe7cd85cc9d104fef
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="configure-or-repair-power-pivot-for-sharepoint-2013"></a>配置或修复 Power Pivot for SharePoint 2013
  若要配置或修复 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 的安装，请使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 配置工具。 该配置工具开始是扫描系统，然后返回完成或修复安装所需的操作列表。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导安装 SharePoint 2010 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具以及 SharePoint 2013 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具。 本主题介绍 SharePoint 2013 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具。 有关 SharePoint 2010 的详细信息，请参阅 [配置或修复 PowerPivot for SharePoint 2010（PowerPivot 配置工具）](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046)。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013  
  
 **本主题内容：**  
  
 [开始之前](#bkmk_before)  
  
 [使用 Power Pivot for SharePoint 2013 配置工具](#bkmk_using)  
  
 [配置步骤](#bkmk_steps)  
  
 [用于配置服务器的输入值](#bkmk_input)  
  
 [后续步骤](#bkmk_nextsteps)  
  
##  <a name="bkmk_before"></a> 开始之前  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具会扫描程序文件、注册表设置和可用端口。 若要充分利用该工具，请先查看以下内容。  
  
-   运行 [Power Pivot Configuration Tools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)的一般要求。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 更适合于创建配置为使用基于声明的身份验证的 Web 应用程序。 如果 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具为您创建了应用程序，则它会将该应用程序配置为使用基于声明的 Windows 身份验证。 有关身份验证要求的详细信息，请参阅 [Power Pivot Authentication and Authorization](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md)。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具必须使用端口 80 才能创建 Web 应用程序。  
  
##  <a name="bkmk_using"></a> 使用 Power Pivot for SharePoint 2013 配置工具  
 该工具的第一页提供了用于配置 SharePoint 场的输入值汇总。 除了您提供的输入值之外，将使用默认值来配置系统。 默认名称用于服务应用程序、服务应用程序数据库和服务应用程序属性。  
  
> [!TIP]  
>  如果该配置工具扫描了计算机并在左窗格中返回一个空白任务列表，则表示没有检测到需要配置的功能或设置。 若要修改 SharePoint 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置，请使用 Windows PowerShell 或 SharePoint 管理中心的管理页。 有关详细信息，请参阅 [在管理中心中管理和配置 PowerPivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)。  
  
 服务帐户的值将用于多个服务。 例如，配置工具使用第一页上的默认帐户来设置所有应用程序池标识。 可以通过在管理中心中修改服务应用程序属性在以后更改这些帐户。  
  
 该工具提供了一个选项卡式界面，其中包括参数输入、Windows PowerShell 脚本和状态消息。  
  
 该工具使用 Windows PowerShell 来配置服务器。 您可以单击 **“脚本”** 选项卡以便查看该工具用于配置服务器的 Windows PowerShell 脚本。  
  
 ![PowerPivot for SharePoint 2013 配置工具](../../analysis-services/power-pivot-sharepoint/media/ssas-powerpivot-configtool-4-sharepoint2013-mainpage-configure.gif "PowerPivot for SharePoint 2013 配置工具")  
  
||Description|  
|-|-----------------|  
|**(1)**|任务列表窗口。|  
|**(2)**|各个操作。|  
|**(3)**|配置工具创建的 Windows PowerShell 脚本。|  
|**(4)**|在您开始验证或运行操作时创建的日志消息。|  
|**(5)**|该页的说明。|  
|**(6)**|输入参数|  
|**(7)**|**“运行”** 按钮将在您验证操作之后启用。|  
  
##  <a name="bkmk_steps"></a> 配置步骤  
 指向该配置工具的链接仅在本地服务器上安装了 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 时才可见。  
  
1.  在“开始”菜单上，指向“所有程序”，然后依次单击 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、“配置工具”和“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置”。  
  
2.  单击“配置或修复 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint”。  
  
3.  将窗口放大为实际大小。 您应该在该窗口的底部看到一个菜单栏，其中包含 **“验证”**、 **“运行”**和 **“退出”** 命令。  
  
4.  **默认帐户：** 在“参数”选项卡上，键入 **“默认帐户用户名”**的域用户帐户。 此帐户用于设置重要服务，包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序池。 不要指定 Network Service 或 Local System 之类的内置帐户。 该工具将阻止指定内置帐户的配置。  
  
     **通行短语：** 键入通行短语。 如果该 SharePoint 场是新场，则在向该 SharePoint 场中添加新的服务器或应用程序时，需要使用该通行短语。 如果该场已存在，则输入允许您向该场添加服务器应用程序的通行短语。  
  
5.  **端口：** 可以选择键入用于连接到管理中心 Web 应用程序的端口号，也可以使用提供的随机生成的端口号。 该配置工具将首先检查该端口号是否可用，然后将其作为选项提供。  
  
6.  在主页上，键入在 SharePoint 模式下运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器的名称。  
  
7.  或者，查看用于完成各操作的剩余输入值。 有关每个输入值的详细信息，请参阅本主题中的 [用于配置服务器的输入值](#bkmk_input) 。  
  
8.  您还可以选择删除不想处理的任何操作。 例如，如果您想要在以后配置 Secure Store Service，则单击 **“配置 Secure Store Service”**，然后清除 **“在任务列表中包括此操作”**复选框。  
  
9. 单击 **“验证”** 以便检查该工具是否有足够的信息来处理列表中的操作。  
  
10. 单击 **“运行”** 来处理该任务列表中的所有操作。 **“运行”** 按钮在您验证操作之后才可用。 如果 **“运行”** 未启用，请首先单击 **“验证”** 。  
  
     如果您看到如下错误消息，请验证该 SQL Server 数据库实例已启动。  
  
    ```  
    Cannot connect to the database server instance  
    ```  
  
11. [Verify a Power Pivot for SharePoint Installation](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)。  
  
##  <a name="bkmk_input"></a> 用于配置服务器的输入值  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具会结合使用您键入的输入值以及它检测到或自动使用的默认值。  
  
 配置工具所显示的操作列表取决于 SharePoint 场的当前配置。 例如，如果已配置 SharePoint 场，则您不会看到用于配置场或创建 Web 应用程序的操作。 您可以随时运行工具以便配置、修复或检测到配置错误。 如果所需服务（例如 Excel Services 或 Secure Store Service）未在场中运行，则该工具会检测到缺失的服务并且提供用于启用这些服务的选项。 如果无需执行任何操作，则任务列表是空的。  
  
 下表说明了用于配置服务器的值。  
  
|第|输入值|数据源|Description|  
|----------|-----------------|------------|-----------------|  
|**配置或修复 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint**|默认帐户|当前用户|默认帐户是用于在场中设置共享服务的域 Windows 用户帐户。 默认帐户用于设置以下项：|  
||||-<br />                    [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序|  
||||-Secure Store Service|  
||||-Excel Services|  
||||-Web 应用程序池标识|  
||||-网站集管理员|  
||||- [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 无人参与的数据刷新帐户。|  
||||默认情况下，使用当前用户的域帐户。<br /><br /> 注意：建议你替换该默认值，除非你配置服务器是为了评估和非生产目的。<br /><br /> 可以使用管理中心在配置或修复后更改服务标识。<br /><br /> 或者，在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具中，为以下项指定专用的帐户：|  
||||-Web 应用程序，使用“创建默认的 Web 应用程序”页（假定该工具正在为场创建 Web 应用程序）。|  
||||-<br />                    [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 无人参与的数据刷新帐户，使用此工具中的 **“为数据刷新创建无人参与的帐户”** 页。|  
||数据库服务器|本地 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 命名实例（如果可用）|如果数据库引擎实例作为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 命名实例安装，则该工具将使用此实例名称填充数据库服务器字段。 如果您没有安装数据库引擎，此字段将为空。<br /><br /> “数据库服务器”  是必需参数。 该实例可以是支持 SharePoint 场的任何 SQL Server 版本或发行版。|  
||通行短语|用户输入|如果您正在创建新的场，则您输入的通行短语将用作该场的通行短语。 如果您正在向现有场添加 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，则键入现有场的通行短语。|  
||SharePoint 管理中心端口|默认值（如果需要）|如果未配置场，则该工具将提供用于创建场的选项，包括创建指向管理中心的 HTTP 端点。 它会选取一个未在使用中的随机生成的端口号。|  
||[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel Services ([服务器名称]\ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])|用户输入|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器是 Excel Services 启用核心 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能所必需的。 你在此页上键入的服务器名称还将添加到“配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器”页上的列表中。|  
|**配置新场**|数据库服务器<br /><br /> 场帐户<br /><br /> 通行短语<br /><br /> SharePoint 管理中心端口|默认值（如果需要）|这些设置默认为在主页上输入的设置。|  
|**创建 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序**|服务应用程序名称|默认|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序名称，默认名称为**默认[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]服务应用程序**。 您可以在该工具中替换为不同的值。|  
||数据库服务器|默认|承载 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库的数据库服务器。 默认服务器名称与用于该场的数据库服务器相同。 您可以将默认服务器名称替换为其他值。|  
||数据库名称|默认|要为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库创建的数据库的名称。 默认数据库名称基于服务应用程序名称，后跟 GUID 以便确保名称唯一。 您可以在该工具中替换为不同的值。|  
|**创建默认的 Web 应用程序**|Web 应用程序名称|默认值（如果需要）|如果不存在任何 Web 应用程序，该工具将创建一个。 Web 应用程序配置为使用经典模式身份验证，并侦听端口 80。 最大文件上载大小设为 2047，这是 SharePoint 所允许的最大值。 较大的文件上载大小用于容纳将上载到服务器的大型 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 文件。|  
||URL|默认值（如果需要）|该工具将基于服务器名称创建一个 URL，并且使用与 SharePoint 相同的文件命名约定。|  
||应用程序池|默认值（如果需要）|该工具在 IIS 中创建默认应用程序池。|  
||应用程序池帐户和密码|默认值（如果需要）|该应用程序池帐户基于默认帐户，但您可以在该工具中替换它。|  
||数据库服务器|默认值（如果需要）|将预先选择默认数据库实例以便存储应用程序内容数据库，但您可以在该工具中指定不同的 SQL Server 实例。|  
||数据库名称|默认值（如果需要）|应用程序数据库的名称。 该数据库名称基于 SharePoint 的文件命名约定，但您可以选择其他名称。|  
|**部署 Web 应用程序解决方案**|URL|默认值（如果需要）|默认 URL 来自默认的 Web 应用程序。|  
||最大文件大小(MB)|默认值（如果需要）|默认设置为 2047。 SharePoint 文档库也有一个最大大小，且 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 设置不应超过此文档库设置。 有关详细信息，请参阅[配置最大文件上传大小 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。|  
|**创建网站集**|网站管理员|默认值（如果需要）|此工具将使用默认帐户。 您可以在 **“创建网站集”** 页中覆盖默认帐户。|  
||联系人电子邮件|默认值（如果需要）|如果在服务器上配置了 Microsoft Outlook，则该工具将使用当前用户的电子邮件地址。 否则，将使用占位符值。|  
||网站 URL|默认值（如果需要）|该工具将创建网站 URL，并且使用与 SharePoint 相同的 URL 命名约定。|  
||网站标题|默认值（如果需要）|此工具将“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 站点”添加为默认标题。|  
|**激活网站集中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能**|网站 URL||激活 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能的网站集的 URL。|  
||为此网站启用高级功能||启用 SharePoint 网站功能“PremiumSite”。|  
|**创建 Secure Store Service 应用程序**|服务应用程序名称|默认值（如果需要）|键入 Secure Store Service 应用程序的名称。|  
||数据库服务器|用户输入|键入用于 Secure Store Service 应用程序的数据库服务器的名称。|  
|**创建 Secure Store Service 应用程序代理**|服务应用程序名称|默认值（如果需要）|键入您在前一页中已键入的 Secure Store Service 应用程序的名称。|  
||服务应用程序代理|默认值（如果需要）|键入 Secure Store Service 应用程序代理的名称。 该名称将出现在默认连接组中，该连接组将应用程序与 SharePoint 内容 Web 应用程序相关联。|  
|**更新 Secure Store Service 主密钥**|服务应用程序代理|默认值（如果需要）|键入您在前一页中已键入的 Secure Store Service 应用程序代理的名称。|  
||通行短语|用户输入|用于数据加密的主密钥。 默认情况下，用于生成密钥的通行短语是用来在场中设置新服务的相同通行短语。 您可以将默认通行短语替换为唯一通行短语。|  
|**为 DataRefresh 创建无人参与的帐户**|目标应用程序 ID|默认值（如果需要）|创建一个目标应用程序，以便存储用于无人参与的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据刷新的凭据。<br /><br /> 应用程序 ID 可以是说明文本。|  
||目标应用程序的友好名称|默认值（如果需要）||  
||无人参与的帐户用户名和密码|默认值（如果需要）|键入由目标应用程序用来运行无人参与数据刷新操作的 Windows 用户帐户的凭据。 有关详细信息，请参阅 [通过在 SharePoint Server 2013 中使用无人参与的服务帐户配置 Excel Services 数据刷新](http://technet.microsoft.com/library/hh525344\(office.15\).aspx) (http://technet.microsoft.com/en-us/library/hh525344(office.15).aspx)。|  
||网站 URL|默认值（如果需要）|键入与目标应用程序关联的网站集的网站 URL。 若要与其他网站集关联，请使用 SharePoint 管理中心。|  
|**创建 Excel Services 服务应用程序**|服务应用程序名称|默认值（如果需要）|键入服务应用程序名称。 将在 SharePoint 场的数据库服务器上创建同名的服务应用程序数据库。|  
|**配置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器**|服务应用程序名称|默认值（如果需要）|您在前一页中键入的服务应用程序名称。|  
||[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器名称||已注册 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器的列表。<br /><br /> 在主页上键入的服务器名称将自动添加到此页。|  
|**将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 外接程序注册为 Excel Services 用法跟踪程序**|服务应用程序名称||您在前一页中键入的服务应用程序名称。|  
|||||  
  
 如果 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具创建该场，它将使用与 SharePoint 相同的文件命名约定在数据库服务器上创建所需的数据库。 不能更改场数据库名称。  
  
 如果该工具创建网站集，它将在数据库服务器上创建内容数据库，并且使用与 SharePoint 相同的文件命名约定。 不能更改内容数据库名称。  
  
## <a name="verify-the-configuration"></a>验证配置  
 请参阅[配置 PowerPivot 和部署解决方案 (SharePoint 2013)](../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)的“验证 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置”部分。  
  
##  <a name="bkmk_nextsteps"></a>后续步骤  
 完成服务器安装后，您应该执行若干安装后任务：  
  
-   将 SharePoint 权限授予各个用户和组。 此任务是启用对站点和内容的访问所必需的。  
  
-   更改服务应用程序池标识符以便在其他帐户下运行。 为服务和应用程序指定不同的标识是实现安全部署的 SharePoint 最佳实践建议。  
  
-   在 Excel Services 中创建其他可信站点，以便您可以改变最适合进行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问的权限和配置设置。  
  
-   安装常用的数据访问接口来启用服务器端数据刷新。  
  
### <a name="grant-sharepoint-permissions-to-workbook-users"></a>向工作簿用户授予 SharePoint 权限  
 用户将首先需要 SharePoint 权限，然后才能发布或查看工作簿。 对需要查看已发布工作簿的用户授予 **“查看”** 权限，对发布或管理工作簿的用户授予 **“参与讨论”** 权限。 您必须是网站集管理员才能授予权限。  
  
1.  在 SharePoint 2013 网站中，单击设置图标![SharePoint 设置](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")，然后单击**站点设置**。  
  
2.  在 **“用户和权限”** 组中单击 **“网站权限”** 。  
  
3.  根据需要创建用户组，例如可以创建一个具有 **“参与”** 权限的用户组，以及一个仅具有 **“查看”** 权限的用户组。  
  
4.  输入分属各个组成员的 Windows 域用户或组帐户。 与前面一样，如果将应用程序配置为采用经典身份验证，则不要使用电子邮件地址或分发组。  
  
### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>安装数据刷新中使用的数据访问接口和检查用户权限  
 服务器端数据刷新使用户可以在无人参与模式下将更新后的数据重新导入到其工作簿中。 为了成功执行数据刷新，在 SharePoint 模式下运行 Analysis Services 的服务器必须具有最初导入数据所用的相同的数据访问接口。 此外，运行数据刷新的用户帐户通常需要对外部数据源具有读取权限。 请务必检查启用和配置数据刷新的要求，以确保获得成功结果。 有关详细信息，请参阅 [使用 SharePoint 2010 进行 Power Pivot 数据刷新](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)。  
  
> [!NOTE]  
>  对于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013，数据访问接口会在运行 **spPowerPivot.msi** 安装程序和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013 配置工具时安装。 有关详细信息，请参阅 [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。  
  
### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>更改 SharePoint 中的应用程序池和服务标识  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 配置工具将场功能、应用程序和服务设置为在单个帐户下运行。 这简化了安装，但会导致部署无法满足 SharePoint 场的安全要求。 若要创建更可靠的部署，请在完成安装后，将应用程序池和服务标识更改为基于不同的帐户运行。 有关详细信息，请参阅 [配置 PowerPivot 服务帐户](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)。  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>在 Excel Services 中创建其他可信站点  
 您可以在 Excel Services 中添加可信站点，以便在提供 Excel 工作簿和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的站点上改变权限和配置设置。 有关详细信息，请参阅 [Create a trusted location for Power Pivot sites in Central Administration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
### <a name="build-a-includessgeminiincludesssgemini-mdmd-workbook"></a>生成 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿  
 在您在场中安装了服务器组件后，可以创建使用嵌入的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的第一个 Excel 2013 工作簿，然后将其发布到 SharePoint 库。 或者，您可以上载或发布示例 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿以验证 SharePoint 中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据访问。 有关详细信息，请参见以下内容：  
  
-   [Power Pivot 帮助](https://support.office.com/en-us/article/Power-Pivot-Help-241aac41-92e3-4e46-ae58-2f2cd7dbcf4f)(https://support.office.com/en-us/article/Power-Pivot-Help-241aac41-92e3-4e46-ae58-2f2cd7dbcf4f)。  
  
-   [在 Excel 2013 外接程序中启动 PowerPivot](http://office.microsoft.com/excel-help/start-powerpivot-in-excel-2013-add-in-HA102837097.aspx?CTT=5&origin=HA102837110) (http://office.microsoft.com/excel-help/start-powerpivot-in-excel-2013-add-in-HA102837097.aspx?CTT=5&origin=HA102837110)。  
  
### <a name="add-additional-analysis-services-servers-in-sharepoint-mode"></a>在 SharePoint 模式下添加其他 Analysis Services 服务器  
 一段时间后，如果您确定需要额外的数据存储和处理能力，则可以向场中添加更多的在 SharePoint 模式下运行 Analysis Services 的服务器。 对于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2013，你可在 SharePoint 模式下安装新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器，然后配置 Excel Services。 有关详细信息，请参阅 [在 PowerPivot 模式下安装 Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)中的“单台服务器安装之外”部分。  
  
## <a name="additional-resources"></a>其他资源  
 ![SharePoint 设置](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 设置")[通过 Microsoft SQL Server Connect 提交反馈和联系信息](https://connect.microsoft.com/SQLServer/Feedback)(https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另请参阅  
 [安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Power Pivot 配置工具](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)   
 [在管理中心中管理和配置 Power Pivot 服务器](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [升级工作簿和计划的数据刷新 (SharePoint 2013)](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  

