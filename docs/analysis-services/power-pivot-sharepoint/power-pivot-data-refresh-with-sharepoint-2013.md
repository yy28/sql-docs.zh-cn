---
title: "Power Pivot 数据刷新与 SharePoint 2013 |Microsoft 文档"
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
ms.assetid: 34f03407-2ec4-4554-b16b-bc9a6c161815
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30482b2c269a3d73bd6ef4852d295ae37e52c5e3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-data-refresh-with-sharepoint-2013"></a>使用 SharePoint 2013 进行 Power Pivot 数据刷新
  SharePoint 2013 中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据模型刷新设计通过利用 Excel Services 作为主组件，加载和刷新在 SharePoint 模式下运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的数据模型。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器在 SharePoint 场的外部运行。 SharePoint 2013 Excel Services 中的体系结构支持“交互式数据刷新”  和“计划数据刷新” 。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013  
  
 **本主题内容：**  
  
-   [交互式数据刷新](#bkmk_interactive_refresh)  
  
-   [带有工作簿数据连接和交互式数据刷新的 Windows 身份验证](#bkmk_windows_auth_interactive_data_refresh)  
  
-   [计划的数据刷新](#bkmk_scheduled_refresh)  
  
-   [SharePoint 2013 中计划的数据刷新体系结构](#bkmk_refresh_architecture)  
  
-   [其他身份验证注意事项](#datarefresh_additional_authentication)  
  
-   [详细信息](#bkmk_moreinformation)  
  
## <a name="background"></a>背景  
 SharePoint Server 2013 Excel Services 管理 Excel 2013 工作簿的数据刷新，并且触发在 SharePoint 模式下运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器上的数据模型处理。 对于 Excel 2010 工作簿，Excel Services 还管理工作簿和数据模型的加载和保存。 但是，Excel Services 依赖于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务将处理命令发送到数据模型。 下表根据工作簿的版本总结了为数据刷新发送处理命令的组件。 假定的环境是 SharePoint 2013 场，它配置为使用在 SharePoint 模式下运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Server。  
  
||||  
|-|-|-|  
||Excel 2013 工作簿|Excel 2010 工作簿|  
|触发数据刷新|**交互：** 经过身份验证的用户<br /><br /> **计划：** [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务|  
|从内容数据库加载工作簿|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|在 Analysis Services 实例上加载数据模型|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|将处理命令发送到 Analysis Services 实例|SharePoint 2013 Excel Services|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务|  
|更新工作簿数据|SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
|将工作簿和数据模型保存到内容数据库|**交互：** 不适用<br /><br /> **计划：** SharePoint 2013 Excel Services|SharePoint 2013 Excel Services|  
  
 下表总结了配置为使用在 SharePoint 模式下运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Server 的 SharePoint 2013 场中支持的刷新功能：  
  
|工作簿的创建位置|计划的数据刷新|交互式刷新|  
|-------------------------|----------------------------|-------------------------|  
|2008 R2 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel|不提供支持。 升级工作簿 **(\*)**|不提供支持。 升级工作簿 **(\*)**|  
|2012 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel|是否支持|不提供支持。 升级工作簿 **(\*)**|  
|Excel 2013|是否支持|是否支持|  
  
 **(\*)** 有关升级工作簿的详细信息，请参阅[升级工作簿和计划的数据刷新 (SharePoint 2013)](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
##  <a name="bkmk_interactive_refresh"></a> 交互式数据刷新  
 SharePoint Server 2013 Excel Services 中的交互式或手动数据刷新可以使用原始数据源中的数据来刷新数据模型。 在您通过注册 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器来配置 Excel Services 应用程序并在 SharePoint 模式下运行后，交互式数据刷新将可用。 有关详细信息，请参阅 [管理 Excel Services 数据模型设置 (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx) (http://technet.microsoft.com/library/jj219780.aspx)。  
  
> [!NOTE]  
>  交互式数据刷新仅可用于在 Excel 2013 中创建的工作簿。 如果你尝试刷新某一 Excel 2010 工作簿，Excel Services 将显示如下错误消息：“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 操作失败: 该工作簿是在较早版本的 Excel 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中创建的，在升级该文件之前无法进行刷新”。 有关升级工作簿的详细信息，请参阅[升级工作簿和计划的数据刷新 (SharePoint 2013)](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
 **交互式刷新的关键相关点：**  
  
-   交互式数据刷新仅刷新当前用户会话中的数据。 这些数据并不自动保存回 SharePoint 内容数据库中的工作簿项。  
  
-   **凭据：** 交互式数据刷新可将当前登录用户的标识作为凭据或存储的凭据来连接到数据源。 所使用的凭据取决于为与外部数据源的工作簿连接而定义的 Excel Services 身份验证设置。  
  
-   **支持的工作簿：**  在 Excel 2013 中创建的工作簿。  
  
 **刷新数据：**  
  
-   请参阅这些步骤之后的图示。  
  
1.  在 SharePoint 文档库中，在浏览器中打开一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿。  
  
2.  在浏览器窗口中，单击 **“数据”** 菜单，然后单击 **“刷新选定的连接”** 或 **“刷新所有连接”**。  
  
3.  Excel Services 将加载 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库，对该数据库进行处理，然后查询该数据库以便刷新 Excel 工作簿缓存。  
  
4.  **注意：** 已更新的工作簿并不自动保存回文档库。  
  
 ![interactive data refresh](../../analysis-services/power-pivot-sharepoint/media/as-interactive-datarefresh-sharepoint2013.gif "interactive data refresh")  
  
###  <a name="bkmk_windows_auth_interactive_data_refresh"></a> 带有工作簿数据连接和交互式数据刷新的 Windows 身份验证  
 Excel Services 向 Analysis Services 服务器发送一个处理命令，该命令指示该服务器模拟某一用户帐户。 为了获取足以执行用户模拟-委托进程的系统权限，该 Analysis Services 服务帐户要求对本地服务器具有“以操作系统方式执行”特权。 该 Analysis Services 服务器还需要能够将用户的凭据委托给数据源。 查询结果被发送到 Excel Services。  
  
 典型用户体验：当某个客户在包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型的 Excel 2013 工作簿中选择“刷新所有连接”时，将会看到如下错误消息：  
  
-   **外部数据刷新失败：** 处理工作簿中的数据模型时出错。 请重试。 无法刷新此工作簿中的一个或多个数据连接。  
  
 根据您正在使用的数据访问接口，将会在 ULS 日志中看到如下消息。  
  
 **对于 SQL Native Client：**  
  
-   无法创建外部连接或执行查询。 提供程序消息：已指定了引用 ID“20102481-39c8-4d21-bf63-68f583ad22bb”的不当对象“DataSource”，但尚未使用。  OLE DB 或 ODBC 错误：与 SQL Server 建立连接时发生了与网络相关的或特定于实例的错误。 找不到或无法访问服务器。 请检查实例名称是否正确以及 SQL Server 是否配置为允许远程连接。 有关详细信息，请参阅 SQL Server 联机丛书。08001；SSL 提供程序：要求的安全包不存在；08001；客户端无法建立连接；08001；客户端不支持加密；08001。  ，ConnectionName：ThisWorkbookDataModel，工作簿：book1.xlsx。  
  
 **对于 Microsoft OLE DB Provider for SQL Server：**  
  
-   无法创建外部连接或执行查询。 提供程序消息：已指定了引用 ID“6e711bfa-b62f-4879-a177-c5dd61d9c242”的不当对象“DataSource”，但尚未使用。 OLE DB 或 ODBC 错误。 ，ConnectionName：ThisWorkbookDataModel，作业簿：OLEDB Provider.xlsx。  
  
 **对于 .NET Framework Data Provider for SQL Server：**  
  
-   无法创建外部连接或执行查询。 提供程序消息：已指定了引用 ID“f5fb916c-3eac-4d07-a542-531524c0d44a”的不当对象“DataSource”，但尚未使用。  高级关系引擎中存在错误。 在使用托管 IDbConnection 接口时，出现以下异常：未能加载文件或程序集“System.Transactions, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089”或它的某一个依赖项。 未提供所需的模拟级别，或提供的模拟级别无效。 (HRESULT 异常: 0x80070542)”。  ，ConnectionName：ThisWorkbookDataModel，工作簿：NETProvider.xlsx。  
  
 **配置步骤摘要** ：若要对本地服务器配置 **“以操作系统方式执行”** 特权，请执行以下操作：  
  
1.  在 SharePoint 模式下运行的 Analysis Services 服务器上，将 Analysis Services 服务帐户添加到“以操作系统方式执行”特权：  
  
    1.  运行“`secpol.msc`”  
  
    2.  依次单击 **“本地安全策略”**、 **“本地策略”**和 **“用户权限分配”**。  
  
    3.  添加该服务帐户。  
  
2.  重新启动 Excel Services 并且重新引导 Analysis Services 服务器。  
  
3.  无需从 Excel Services 服务帐户或声明为 Windows 令牌服务 (C2WTS) 到 Analysis Services 实例的委托。 因此，无需针对从 Excel Services 或 C2WTS 到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务的 KCD 的配置。 如果数据源与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例位于同一台服务器上，则不需要 Kerberos 约束委派。 但是， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务帐户需要“以操作系统方式执行”权限。  
  
 ![as_interactive_data_refresh2012SP1_windowsauth](../../analysis-services/power-pivot-sharepoint/media/as-interactive-data-refresh2012sp1-windowsauth.gif "as_interactive_data_refresh2012SP1_windowsauth")  
  
 有关详细信息，请参阅 [以操作系统方式执行](http://technet.microsoft.com/library/cc784323\(WS.10\).aspx) (http://technet.microsoft.com/library/cc784323(WS.10).aspx)。  
  
##  <a name="bkmk_scheduled_refresh"></a> 计划的数据刷新  
 **计划的数据刷新的关键相关点：**  
  
-   要求部署 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 外接程序。 有关详细信息，请参阅[安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2013)](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。  
  
-   用户为工作簿配置刷新计划。 在计划的时间， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务将一个请求发送到 Excel Services 以便：  
  
    -   加载和处理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库。  
  
    -   刷新工作簿。  
  
    -   将该工作簿保存回内容数据库。  
  
-   **凭据：** 使用存储的凭据。 不要使用当前用户的标识。  
  
-   **支持的工作簿：** 使用 Excel 2010 的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 外接程序或使用 Excel 2013 创建的工作簿。 不支持在具有 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 外接程序的 Excel 2010 中创建的工作簿。 请将工作簿升级到至少是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 格式。 有关升级工作簿的详细信息，请参阅[升级工作簿和计划的数据刷新 (SharePoint 2013)](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
 要显示 **“管理数据刷新”** 页，请执行以下操作：  
  
-   请参阅这些步骤之后的图示。  
  
1.  在 SharePoint 文档库中，为某个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿单击“打开菜单 (**...**)”。  
  
2.  单击第二个“打开菜单”，然后单击“管理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据刷新”。  
  
3.  在 **“管理数据刷新”** 页上，单击 **“启用”** ，然后配置刷新计划。  
  
4.  在指定的时间， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务将一个请求发送到 Excel Services 以便：  
  
    -   加载和处理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据模型。  
  
    -   刷新工作簿。  
  
    -   将该工作簿保存回内容数据库。  
  
 ![管理数据刷新上下文菜单](../../analysis-services/power-pivot-sharepoint/media/as-manage-datarefresh-sharepoint2013.gif "管理数据刷新上下文菜单")  
  
> [!TIP]  
>  有关从 SharePoint Online 刷新工作簿的信息，请参阅 [使用内置的 Power Pivot 模型从 SharePoint Online 刷新 Excel 工作簿（白皮书）](http://technet.microsoft.com/library/jj992650.aspx) (http://technet.microsoft.com/library/jj992650.aspx)。  
  
##  <a name="bkmk_refresh_architecture"></a> SharePoint 2013 中计划的数据刷新体系结构  
 下图总结了 SharePoint 2013 和 SQL Server 2012 SP1 中的数据刷新体系结构。  
  
 ![SQL Server 2012 SP1 数据刷新体系结构](../../analysis-services/power-pivot-sharepoint/media/as-scheduled-data-refresh2012sp1-architecture.gif "的 SQL Server 2012 SP1 数据刷新体系结构")  
  
||Description||  
|-|-----------------|-|  
|**(1)**|Analysis Services 引擎|在 SharePoint 模式下运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器上的数据模型处理。 该服务器在 SharePoint 场的外部运行。|  
|**(2)**|用户界面|该用户界面由两页构成。 一页用于定义计划，另一页用于查看刷新历史记录。 这两页并不直接访问 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库，而是使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务访问这些数据库。|  
|**(3)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务|在部署 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 外接程序时安装该服务。<br /><br /> 该服务用于以下目的：|  
|||该服务承载刷新计划引擎，该引擎调用 Excel Services API 以便进行 Excel 2013 工作簿的数据刷新。 对于 Excel 2010 工作簿，该服务直接执行数据模型处理，但继续依赖 Excel Services 加载数据模型和更新工作簿。|  
|||该服务为组件（例如用户界面页）提供与系统服务进行通信的方法。|  
|||管理对作为数据源的工作簿的外部访问的请求，这些请求是通过 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Web 服务接收的。|  
|||对计时器作业和配置页的计划的数据刷新请求管理。 该服务管理从服务应用程序数据库读入和读出数据的请求，并且使用 Excel Services 触发数据刷新。|  
|||使用情况处理和相关计时器作业。|  
|**(4)**|Excel 计算服务|负责加载数据模型。|  
|**(5)**|Secure Store Service|如果工作簿中的身份验证设置配置为 **“使用已经过身份验证的用户的帐户”** 或 **“无”**，则在安全存储区目标应用程序 ID 中存储的凭据将用于数据刷新。 有关详细信息，参阅本主题中的 [其他身份验证注意事项](#datarefresh_additional_authentication) 部分。|  
|**(6)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据刷新计时器作业|指示 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务与 Excel Services 进行连接以便刷新数据模型。|  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 要求适当的数据访问接口和客户端库，以便处于 SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器可以访问数据源。  
  
> [!NOTE]  
>  因为 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务不再加载或保存 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型，所以用于在应用程序服务器上缓存模型的大多数设置不适用于 SharePoint 2013 场。  
  
## <a name="data-refresh-log-data"></a>数据刷新日志数据  
 **使用情况数据：** 你可以在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板中查看数据刷新使用情况数据。 要查看使用情况数据，请执行以下操作：  
  
1.  在 SharePoint 管理中心中，在“常规应用程序设置”组中单击“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板”。  
  
2.  在该面板的底部，查看 **“数据刷新 - 最近的活动”** 和 **“数据刷新 - 最近的失败”**。  
  
3.  有关使用情况数据以及如何启用它的详细信息，请参阅 [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)。  
  
 **诊断日志数据：** 您可以查看与数据刷新相关的 SharePoint 诊断日志数据。 首先，在 SharePoint 管理中心的“监视”页中确认针对“[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务”的诊断日志记录的配置。 对于要记入日志的“严重程度最低的事件”，您可能需要增加日志记录的级别。 例如，暂时将该值设置为 **“详细”** ，然后重新运行数据刷新操作。  
  
 日志项包含：  
  
-   **服务** 的 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 区域**。  
  
-   “数据刷新” 的类别。  
  
 查看 **“配置诊断日志记录”**。 有关详细信息，请参阅[配置和查看 SharePoint 日志文件和诊断日志记录 (Power Pivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)。
  
##  <a name="datarefresh_additional_authentication"></a> 其他身份验证注意事项  
 在 Excel 2013 中， **“Excel Services 身份验证设置”** 对话框中的设置确定 Excel Services 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用于数据刷新的 Windows 标识。  
  
-   **使用已经过身份验证的用户的帐户**：Excel Services 基于当前登录的用户的标识执行数据刷新。  
  
-   **使用存储的帐户**：假定为 SharePoint Secure Store Service 应用程序 ID，Excel Services 使用该 ID 检索用户名和密码，以便对数据刷新进行身份验证。  
  
-   **无**：使用 Excel Services 的 **“无人参与服务帐户”** 。 该服务帐户与某一安全存储区代理相关联。 在 **“Excel Services 应用程序设置”** 页上配置 **“外部数据”** 部分中的设置。  
  
 打开身份验证设置对话框：  
  
1.  在 Excel 2013 中单击 **“数据”** 选项卡。  
  
2.  在功能区中单击 **“连接”** 。  
  
3.  在 **“工作簿连接”**对话框中，选择连接，然后单击 **“属性”**。  
  
4.  在 **“连接属性”** 对话框中，单击 **“定义”**，然后单击 **“身份验证设置…”** 按钮。  
  
 ![excel services authentication settings](../../analysis-services/power-pivot-sharepoint/media/as-authentication-settings-4-ecs-in-excel2013.gif "excel services authentication settings")  
  
 有关数据刷新身份验证和凭据用法的详细信息，请参阅博客文章 [在 SharePoint 2013 中刷新 Power Pivot 数据](http://blogs.msdn.com/b/analysisservices/archive/2012/12/21/refreshing-powerpivot-data-in-sharepoint-2013.aspx)。  
  
##  <a name="bkmk_moreinformation"></a> 详细信息  
 [Power Pivot 数据刷新故障排除](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx)。  
  
 [SharePoint 2013 中的 Excel Services](http://msdn.microsoft.com/library/sharepoint/jj164076\(v=office.15\)) (http://msdn.microsoft.com/library/sharepoint/jj164076(v=office.15))。  
  
## <a name="see-also"></a>另请参阅  
 [在 Power Pivot 模式下安装 Analysis Services。](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  

