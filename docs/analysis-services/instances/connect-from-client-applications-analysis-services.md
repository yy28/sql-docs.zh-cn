---
title: 连接客户端应用程序 (Analysis Services) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d71320fad55b9a0d052ad1bb9c9fd25ab861246c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748639"
---
# <a name="connect-from-client-applications-analysis-services"></a>从客户端应用程序进行连接 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果您不熟悉 Analysis Services，则在了解了本主题中的信息之后，您就可以通过常用工具和应用程序连接到现有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。 本主题还说明如何出于测试目的基于不同的用户标识进行连接。  
  
-   [使用 SQL Server Management Studio (SSMS) 进行连接](#bkmk_SSMS)  
  
-   [使用 Excel 进行连接](#bkmk_excel)  
  
-   [使用 SQL Server Data Tools 进行连接](#bkmk_SSDT)  
  
-   [测试连接](#bkmk_tshoot)  
  
 连接字符串参考文档单独提供。 有关详细信息，请参阅[连接字符串属性 (Analysis Services)](../../analysis-services/instances/connection-string-properties-analysis-services.md)。  
  
 成功的连接依赖于有效的端口配置和适当的用户权限。 要了解有关各项要求的详细信息，请单击以下链接。  
  
-   [配置 Windows 防火墙以允许 Analysis Services 访问](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [授予对对象和操作的访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> 使用 SQL Server Management Studio (SSMS) 进行连接  
 在 SSMS 中连接到 Analysis Services 时，能够以交互方式管理服务器实例和数据库。 还可以运行 XMLA 或 MDX 查询以便执行管理任务或检索数据。 与只在发出查询时才加载数据库的其他工具和应用程序相比，SSMS 会在您连接服务器时加载所有数据库，前提是您拥有查看数据库的权限。 这意味着，如果您在服务器上保存有大量的表格数据库，所有这些数据库都会在您使用 SSMS 连接时加载至系统内存。  
  
 您可以通过在特定用户标识下运行 SSMS、然后作为该用户连接到 Analysis Services，对权限进行测试。  
  
 按住 Shift 键并右键单击 **SQL Server Management Studio** 快捷方式，以便访问“以其他用户身份运行”选项。  
  
1.  启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 在 **“连接到服务器”** 对话框中，选择 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器类型。  
  
2.  在“登录”选项卡中，通过键入运行服务器的计算机的名称来输入服务器名称。 可以使用服务器的网络名称或完全限定域名指定服务器。  
  
     对于命名实例，必须以 servername\instance name 格式指定服务器名称。 此命名约定的示例可以是网络名称为 ADV-SRV062 的服务器的 ADV-SRV062\Finance，其中，已将 Analysis Services 作为标题为 Finance 的命名实例安装。  
  
     对于部署在故障转移群集中的服务器，请使用 SSAS 群集的网络名称建立连接。 此名称在 SQL Server 安装期间指定，名为 **“SQL Server 网络名称”**。 请注意，如果您将 SSAS 以命名实例形式安装到 Windows Server 故障转移群集 (WSFC) 上，则绝不要在连接上添加实例名称。 这一做法仅适用于 SSAS；相比之下，群集关系数据库引擎的命名实例包含实例名称。 例如，如果您将 SSAS 和数据库引擎均安装为命名实例 (Contoso-Accounting)，SQL Server 网络名称为 SQL-CLU，则需使用“SQL-CLU”连接 SSAS，而使用“SQL-CLU\Contoso-Accounting”来连接数据库引擎。 有关更多信息和示例，请参阅 [如何安装群集 SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=396548) 。  
  
     对于部署在网络负载平衡群集中的服务器，请使用 NLB 的虚拟服务器名称建立连接。  
  
3.  身份验证始终为 Windows 身份验证，并且用户标识始终为通过 Management Studio 进行连接的 Windows 用户。  
  
     为了能成功连接，您必须拥有对服务器或服务器上的数据库的访问权限。 您想要在 Management Studio 中执行的大多数任务都要求管理权限。 请确保您用来进行连接的帐户是服务器管理员角色的成员。 有关详细信息，请参阅 [向 Analysis Services 实例授予服务器管理员权限](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
4.  单击 **“连接属性”** 以便指定特定数据库、设置超时值或加密选项。 可选连接信息包含仅用于当前连接的连接属性。  
  
5.  单击 **“其他连接参数”** 选项卡以便设置在“连接到服务器”对话框中未提供的连接属性。 例如，您可以在文本框中键入 `Roles=Reader` 。  
  
     通过具有较少权限的角色进行连接使您可以测试该角色起作用时的数据库行为。  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> 使用 Excel 进行连接  
 Microsoft Excel 通常用于对业务数据进行分析。 作为 Excel 安装的一部分，Office 将安装 Analysis Services OLE DB 访问接口 (MSOLAP DLL)、ADOMD.NET 和其他数据访问接口，使您能够更轻松地使用网络服务器上的数据。 如果您使用的是较新版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和较旧版本的 Excel，则很可能需要在连接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的每台工作站上安装较新的数据提供程序。 有关详细信息，请参阅 [用于 Analysis Services 连接的数据提供程序](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md) 。  
  
 在设置与 Analysis Services 多维数据集或表格模型数据库的连接时，Excel 会将连接信息保存到 .odc 文件中以供将来使用。 该连接是在当前 Windows 用户的安全上下文中创建的。 为了能成功连接，该用户帐户必须具有数据库的读取权限。  
  
 在 Excel 工作簿中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据时，查询请求期间将一直保持连接。 因此，从 Excel 监视查询工作负荷时，您很可能发现每个会话都存在大量持续时间很短的连接。  
  
 您可以通过基于特定的用户标识启动 Excel 来测试权限。  
  
 按住 Shift 键并右键单击 **Excel** 快捷方式，以便访问“以其他用户身份运行”选项。  
  
1.  在 Excel 的“数据”选项卡上，单击 **“自其他来源”**，然后单击 **“来自 Analysis Services”**。 输入服务器名称，然后选择要查询的多维数据集或透视。  
  
     对于部署在负载平衡群集中的服务器，请使用分配给该群集的虚拟服务器名称。  
  
2.  在 Excel 中设置连接时，可以在数据连接向导的最后一页上指定 Excel Services 的身份验证设置。 这些设置用于设置应上载到包含 Excel Services 的 SharePoint 服务器的工作簿的属性。 数据刷新操作中会使用这些设置。 选项包括“Windows 身份验证”、“Secure Store Service”(SSS) 和“无”。  
  
     避免使用 **“无”**。 除非您连接到已配置 HTTP 访问的服务器，否则，Analysis Services 将不允许您在连接字符串上指定用户名和密码。 同样，除非您知道 SSS 目标应用程序 ID 将映射到一组拥有对 Analysis Services 数据库的用户访问权限的 Windows 用户凭据，否则不要使用 SSS。 在大多数方案中，对于来自 Excel 的 Analysis Services 连接，最佳选择是使用 Windows 身份验证的默认选项。  
  
 有关详细信息，请参阅 [连接到 SQL Server Analysis Services 或从其中导入数据](http://go.microsoft.com/fwlink/?linkID=215150)。  
  
##  <a name="bkmk_SSDT"></a> 使用 SQL Server Data Tools 进行连接  
 SQL Server Data Tools 用于生成 BI 解决方案，包括 Analysis Services 模型、Reporting Services 报表和 SSIS 包。 在生成报表或包时，您可能需要指定与 Analysis Services 的连接。  
  
 下面的链接说明如何从报表服务器项目或 Integration Services 项目连接到 Analysis Services：  
  
-   [针对 MDX 的 Analysis Services 连接类型 (SSRS)](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Analysis Services 连接管理器](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  在使用 SQL Server Data Tools 处理现有 Analysis Services 项目时，请记住您可以使用本地或版本控制项目脱机连接，或者在联机模式下进行连接以便在数据库正运行时更新 Analysis Services 对象。 有关详细信息，请参阅 [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)。 更常见的情况是，来自 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的连接将处于项目模式下，这样一来，只有在您显式部署项目时才能将更改部署到数据库。  
  
##  <a name="bkmk_tshoot"></a> 测试连接  
 您可以使用 SQL Server Profiler 来监视与 Analysis Services 的连接。 Audit Login 和 Audit Logout 事件提供连接证据。 标识列指示进行连接所基于的安全上下文。  
  
1.  在 Analysis Services 实例上启动 **SQL Server Profiler** ，然后开始一个新跟踪。  
  
2.  在“事件选择”中，确认在“安全审核”部分中选中了 **Audit Login** 和 **Audit Logout** 。  
  
3.  通过某一应用程序服务（例如 SharePoint 或 Reporting Services）从远程客户端计算机连接到 Analysis Services。 Audit Login 事件将显示连接到 Analysis Services 的用户的标识。  
  
 连接错误常常源于不完整或无效的服务器配置。 应始终首先检查服务器配置：  
  
-   从远程计算机对服务器执行 Ping 操作以便确保它允许远程连接。  
  
-   **服务器上的防火墙规则允许来自相同域中客户端的入站连接**  
  
     除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 之外，所有与远程服务器的连接都要求你将防火墙配置为允许访问 Analysis Services 正在侦听的端口。 如果您遇到连接错误，请验证端口是否可访问以及是否授予对相应数据库的用户权限。  
  
     若要进行测试，请在远程计算机上使用 Excel 或 SSMS，并且指定 Analysis Services 实例使用的 IP 地址和端口。 如果您可以连接，则防火墙规则对实例是有效的并且实例允许远程连接。  
  
     此外，在使用 TCP/IP 作为连接协议时，请记住 Analysis Services 要求客户端连接源自相同的域或可信域。 如果连接穿过了安全边界，您很可能需要配置 HTTP 访问。 有关详细信息，请参阅 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
-   某些工具可以连接，而其他工具却不能？ 该问题可能是客户端库的版本错误导致的。 您可以从 SQL Server 功能包下载页获取客户端库。  
  
 可帮助您解决连接失败的资源包括以下资源：  
  
 [解决 SQL Server 2005 Analysis Services 连接方案中的常见连接问题](http://technet.microsoft.com/library/cc917670.aspx)。 本文档是几年前撰写的，但文中提及的信息和方法现在仍然适用。  
  
## <a name="see-also"></a>请参阅  
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Analysis Services 支持的身份验证方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [模拟](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   
 [创建数据源（SSAS 多维）](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
