---
title: 针对 Kerberos 约束委派配置 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3436b2d0e73fc452c12e1aa5a71724e9f8dcd31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191307"
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Kerberos 约束委派配置 Analysis Services
  在配置 Analysis Services 以使用 Kerberos 身份验证时，您很可能希望实现以下两个结果中的一个或全部两个：在查询数据时让 Analysis Services 模拟某个用户标识；或者让 Analysis Services 将某个用户标识委托给下级服务。 每个方案都具有稍有不同的配置要求。 这两个方案都要求进行验证，以便确保正确完成配置。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一款诊断工具，可帮助解决与 Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相关的连接问题。 有关详细信息，请参阅 [Microsoft Kerberos Configuration Manager for SQL Server](http://www.microsoft.com/download/details.aspx?id=39046)。  
  
 本主题包含以下各节：  
  
-   [允许 Analysis Services 模拟某个用户标识](#bkmk_impersonate)  
  
-   [配置 Analysis Services 以实现可信委托](#bkmk_delegate)  
  
-   [测试模拟的标识或委托的标识](#bkmk_test)  
  
> [!NOTE]  
>  如果与 Analysis Services 的连接是单跃点，或者您的解决方案使用 SharePoint Secure Store Service 或 Reporting Services 提供的存储的凭据，则委托不是必需的。 如果所有连接都是从 Excel 到 Analysis Services 数据库的直接连接或是以存储的凭据为基础，则可以直接使用 Kerberos（或 NTLM）而无需配置约束委托。  
>   
>  如果用户标识必须流经多个计算机连接（称为“双跃点”），则需要使用 Kerberos 约束委托。 在 Analysis Services 数据访问针对用户标识是有条件的，并且连接请求来自某一委托服务，则使用下一节中的核对清单确保 Analysis Services 能够模拟原始调用方。 有关 Analysis Services 身份验证流的详细信息，请参阅 [Microsoft BI 身份验证和身份委托](http://go.microsoft.com/fwlink/?LinkID=286576)。  
>   
>  作为一项最佳安全配置，Microsoft 始终建议约束委派而不是非约束委派。 由于非约束委托允许服务标识在 *任何* 下游计算机、服务或应用程序上模拟另一个用户（正好与那些经由约束委托明确定义的服务相反），因此是一个主要的安全风险。  
  
##  <a name="bkmk_impersonate"></a> 允许 Analysis Services 模拟某个用户标识  
 为了允许上级服务（例如 Reporting Services、IIS 或 SharePoint）模拟 Analysis Services 上的用户标识，您必须针对这些服务配置 Kerberos 约束委派。 在此方案中，Analysis Services 使用委托服务提供的标识模拟当前用户，并且基于该用户标识的角色成员身份返回结果。  
  
|任务|Description|  
|----------|-----------------|  
|步骤 1：确认帐户是否适合委托|请确保用于运行服务的帐户在 Active Directory 中具有正确的属性。 Active Directory 中的服务帐户不得标记为敏感帐户，也不得明确从委托方案中排除。 有关详细信息，请参阅 [理解用户帐户](http://go.microsoft.com/fwlink/?LinkId=235818)。<br /><br /> **\*\* 重要\* \* **所有帐户和服务器必须通常情况下，都属于同一 Active Directory 域或者同一个林中受信任的域。 但是，因为 Windows Server 2012 支持跨域边界的委托，如果域功能级别是 Windows Server 2012，您可以配置跨域边界的 Kerberos 约束委派。 另一种替代方法是，配置 Analysis Services 进行 HTTP 访问并对客户端连接使用 IIS 身份验证方法。 有关详细信息，请参阅[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](configure-http-access-to-analysis-services-on-iis-8-0.md)。|  
|步骤 2：注册 SPN|在设置约束委派前，您必须为 Analysis Services 实例注册服务主体名称 (SPN)。 在为中间层服务配置 Kerberos 约束委派时，将需要 Analysis Services SPN。 有关说明，请参阅 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md) 。<br /><br /> 服务主体名称 (SPN) 指定域中为 Kerberos 身份验证配置的服务的唯一标识。 使用集成安全性的客户端连接通常请求 SPN 作为 SSPI 身份验证的一部分。 该请求被转发到 Active Directory 域控制器 (DC)，并且由 KDC 授予一个票证（如果客户端提供的 SPN 在 Active Directory 中有匹配的 SPN 注册）。|  
|步骤 3：配置约束委派|在验证要使用的帐户和为这些帐户注册 SPN 后，下一步是为约束委派配置上级服务（例如 IIS、Reporting Services 或 SharePoint Web 服务），并且将 Analysis Services SPN 作为允许委托的特定服务列出。<br /><br /> 在 SharePoint 中运行的服务（例如 SharePoint 模式下的 Excel Services 或 Reporting Services）常常承载使用 Analysis Services 多维或表格数据的工作簿和报表。 为这些服务配置约束委派是一个常见的配置任务，并且是支持从 Excel Services 执行数据刷新所必需的。 以下链接提供 SharePoint 服务以及其他服务的说明，这些服务可能存在针对 Analysis Services 数据的下游数据连接请求：<br /><br /> [Excel Services 的标识委托 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299826) 或 [如何配置 SharePoint Server 2010 中的 Excel Services 的 Kerberos 身份验证](http://support.microsoft.com/kb/2466519)<br /><br /> [针对 PerformancePoint Services 的标识委托 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [针对 SQL Server Reporting Services 的标识委托 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> 对于 IIS 7.0，请参阅 [配置 Windows 身份验证 (IIS 7.0)](http://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) 或 [如何配置 SQL Server 2008 Analysis Services 和 SQL 服务器 2005 Analysis Services 使用 Kerberos 身份验证](http://support.microsoft.com/kb/917409)。|  
|步骤 4：测试连接|测试时，请基于不同标识从远程计算机连接，并使用与业务用户相同的应用程序来查询 Analysis Services。 您可以使用 SQL Server Profiler 来监视连接。 您应该会看到发出请求的用户标识。 有关详细信息，请参阅本节中的 [测试模拟的标识或委托的标识](#bkmk_test) 。|  
  
##  <a name="bkmk_delegate"></a> 配置 Analysis Services 以实现可信委托  
 通过将 Analysis Services 配置为使用 Kerberos 约束委派，可允许服务模拟下级服务（例如关系数据库引擎）上的客户端标识，然后就可以像直接连接客户端一样查询数据。  
  
 针对 Analysis Services 的委托方案被限制为针对 `DirectQuery` 模式配置的表格模型。 这是 Analysis Services 可以将委托的凭据传递到其他服务的唯一情形。 在所有其他情形中（如在前一节中提到的 SharePoint 情形），Analysis Services 位于委托链的接受端。 有关 DirectQuery 的详细信息，请参阅[DirectQuery 模式（SSAS 表格）](../tabular-models/directquery-mode-ssas-tabular.md)。  
  
> [!NOTE]  
>  一个常见的误解是 ROLAP 存储、处理操作或对远程分区的访问会以某种方式引入对约束委托的要求。 事实并非如此。 所有这些操作均由服务帐户（也称为处理帐户）代表其自身来直接执行。 在 Analysis Services 中，如果将这些操作的权限直接授予该服务帐户（例如，授予关系数据库的 db_datareader 权限以便服务可以处理数据），则这些操作无需委托。 有关服务器操作和权限的详细信息，请参阅[配置服务帐户 (Analysis Services)](configure-service-accounts-analysis-services.md)。  
  
 本节说明如何针对信任的委托设置 Analysis Services。 在您完成此任务后，Analysis Services 将能够将委托的凭据传递给 SQL Server，以支持在表格解决方案中使用的 DirectQuery 模式。  
  
 准备工作：  
  
-   确认启动了 Analysis Services。  
  
-   确认为 Analysis Services 注册的 SPN 有效。 有关说明，请参阅 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)。  
  
 在两个先决条件均得到满足后，继续执行以下步骤。 请注意，若要设置约束委派，您必须是域管理员。  
  
1.  在“Active Directory 用户和计算机”中，找到 Analysis Services 按其运行的服务帐户。 右键单击该服务帐户，然后选择 **“属性”**。  
  
     出于说明目的，以下屏幕快照使用 OlapSvc 和 SQLSvc 分别表示 Analysis Services 和 SQL Server。  
  
     OlapSvc 是为针对 SQLSvc 的约束委派将配置的帐户。 在您完成此任务后，OlapSvc 将有权将服务票证上的委托的凭据传递给 SQLSvc，并且在请求数据时模拟原始调用方。  
  
2.  在“委托”选项卡上，选择 **“仅信任此用户对指定服务的委托”**，后跟 **“仅使用 Kerberos”**。 单击“添加”  以指定允许 Analysis Services 委托凭据的服务。  
  
     只有在将用户帐户 (OlapSvc) 分配给某一服务 (Analysis Services) 并且为该服务注册了 SPN 的情况下，“委托”选项卡才会出现。 SPN 注册要求该服务正在运行。  
  
     ![SSAS_Kerberos_1_AccountProperties](../media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  在“添加服务”页上，单击 **“用户或计算机”**。  
  
     ![SSAS_Kerberos_2_](../media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  在“选择用户或计算机”页上，输入用于运行 SQL Server 实例并且向 Analysis Services 表格模型数据库提供数据的帐户。 单击 **“确定”** 接受该服务帐户。  
  
     如果您不能选择想要的帐户，则确认 SQL Server 正在运行并且为该帐户注册了 SPN。 有关针对数据库引擎的 SPN 的详细信息，请参阅 [Register a Service Principal Name for Kerberos Connections](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。  
  
     ![SSAS_Kerberos_3_SelectUsers](../media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  该 SQL Server 实例现在应出现在“添加服务”中。 也在使用该帐户的任何服务也将出现在该列表中。 选择您要使用的 SQL Server 实例。 单击 **“确定”** 接受该实例。  
  
     ![SSAS_Kerberos_4_](../media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  该 Analysis Services 服务帐户的属性页现在应类似于以下屏幕快照。 单击 **“确定”** 保存所做的更改。  
  
     ![SSAS_Kerberos_5_Finished](../media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  通过基于不同标识从远程客户端计算机进行连接来测试委托是否成功和查询表格模型。 您应在 SQL Server Profiler 中看到针对请求的用户标识。  
  
##  <a name="bkmk_test"></a> 测试模拟的标识或委托的标识  
 使用 SQL Server Profiler 可监视正查询数据的用户的标识。  
  
1.  在 Analysis Services 实例上启动 **SQL Server Profiler** ，然后开始一个新跟踪。  
  
2.  在事件选择确认`Audit Login`和`Audit Logout`安全审核部分中选中了。  
  
3.  通过某一应用程序服务（例如 SharePoint 或 Reporting Services）从远程客户端计算机连接到 Analysis Services。 Audit Login 事件将显示连接到 Analysis Services 的用户的标识。  
  
 彻底的测试将要求使用可捕获网络上的 Kerberos 请求和响应的网络监视工具。 针对 Kerberos 筛选的网络监视器实用工具 (netmon.exe) 可用于此任务。 有关使用 Netmon 3.4 和测试 Kerberos 身份验证所用的其他工具的详细信息，请参阅 [配置 Kerberos 身份验证：核心配置 (SharePoint Server 2010)](http://technet.microsoft.com/library/gg502602\(v=office.14\).aspx)。  
  
 另外，请参阅 [Active Directory 中最易令人混淆的对话框](http://windowsitpro.com/windows/most-confusing-dialog-box-active-directory) ，查看对 Active Directory 对象的属性对话框的“委托”选项卡中对每个选项的详尽描述。 这篇文章也说明了如何使用 LDP 测试和解释测试结果。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft BI 身份验证和身份委托](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [使用 Kerberos 进行相互身份验证](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [连接到 Analysis Services](connect-to-analysis-services.md)   
 [针对 Analysis Services 实例的 SPN 注册](spn-registration-for-an-analysis-services-instance.md)   
 [连接字符串属性&#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)  
  
  
