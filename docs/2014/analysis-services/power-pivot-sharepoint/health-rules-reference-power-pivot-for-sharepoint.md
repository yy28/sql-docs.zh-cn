---
title: 运行状况规则参考 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 47ae04ce-7b9d-49c2-8dbc-bafcb73d4603
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60d8599942db1c7f1ff679d92de496692ed2d58b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071394"
---
# <a name="health-rules-reference-powerpivot-for-sharepoint"></a>运行状况规则参考 (PowerPivot for SharePoint)
  本参考主题说明由 PowerPivot for SharePoint 安装添加的 SharePoint 运行状况规则。 这些规则用于报告有关 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务应用程序或其关联的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的服务器运行状况、可用性或配置问题。  
  
 下表按规则在 SharePoint 管理中心的“运行状况分析器规则定义”页中显示的顺序列出这些规则。 对于可配置的规则，您可以更改触发规则的阈值。 有关详细信息，请参阅[PowerPivot 运行状况规则-配置](configure-power-pivot-health-rules.md)。 “自动修复”指示有内置解决方法可以解决问题，您可以从“问题报告”页单击该方法。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 | SharePoint 2010|  
  
 **注意：** [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 对不同版本的 SharePoint 安装不同的运行状况规则集。 请参阅下，表中的"版本"列，或可以运行以下 Windows PowerShell 命令以查看已安装的规则。  
  
```  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like "*power*"}  | format-table -property * -autosize | out-default  
```  
  
|规则|可配置|自动修复|版本|Description|  
|----------|------------------|-----------------|-------------|-----------------|  
|PowerPivot:在此计算机上未安装 Analysis Services OLE DB 提供程序。|否|否|SharePoint 2010|Analysis Services OLE DB 访问接口未安装在服务器上或版本错误。 当 SharePoint 场包含不具有 PowerPivot for SharePoint 的应用程序服务器上的 Excel Services 实例时，显示此规则。 此规则警告未安装 Excel Services 用于连接到 PowerPivot 数据的 Analysis Services OLE DB 访问接口。 要解决此问题，请在不具有 Analysis Services OLE DB 访问接口的每个 Excel Services 服务器上安装 OLE DB 访问接口。 可以从 Microsoft 下载中心下载并安装 Analysis Services OLE DB 访问接口。 有关详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。|  
|PowerPivot:在此计算机上安装 MSOLAP 提供程序的 SQL Server 2008 R2 版本后，针对 Microsoft.AnalysisServices.ChannelTransport.dll 的注册表设置均无效。|否|是|SharePoint 2010|这是服务器配置问题。 很可能 ChannelTransport.dll 未在全局程序集中注册。 在安装 PowerPivot for SharePoint 的每个服务器上运行此规则的自动修复以注册 .dll。 或者，也可以手动运行 regasm.exe 以注册该文件。 如果 SharePoint 计时器服务未作为本地管理员运行，必须进行手动注册。 更新注册表设置失败将导致 Excel Services 和 PowerPivot 系统服务之间的服务器通信缓慢，并可以导致某些安全配置下的连接失败。|  
|PowerPivot:PowerPivot 服务应用程序没有权限，才能完成操作。|否|否|SharePoint 2010|此规则检查 PowerPivot 服务应用程序标识是否是 PowerPivot 服务器应用程序数据库的数据库所有者，以及是否具有对本地 SQL Server Analysis Services 实例的管理权限。 这些权限在安装和部署过程中自动授予，但如果此步骤未能完成，将发生此运行状况规则。|  
|PowerPivot:PowerPivot 服务应用程序标识不应是本地 Administrators 组的成员。|否|否|SharePoint 2010|这是提高您的部署的总体安全性的最佳做法。 如果您配置了 PowerPivot 服务应用程序在属于本地 Administrator 组的帐户下运行，应将该服务帐户更改为不属于该组的帐户。 建议对每个服务使用最低特权的专用帐户。 这样做将提供服务隔离并便于审核登录。 有关更改服务帐户的详细信息，请参阅[配置 PowerPivot 服务帐户](configure-power-pivot-service-accounts.md)。|  
|PowerPivot:Analysis Services 实例在表格模式下运行，但指定此模式的配置设置处于关闭状态。|否|否|SharePoint 2010|此规则检查 PowerPivot for SharePoint 安装中的 SQL Server Analysis Services 实例是否将 `DeploymentMode` 服务器属性设置为 1。 如果将该属性设置为其他值，或如果运行规则检查器的 SharePoint 计时器服务不具有打开文件的权限，此规则将失败。 有关部署模式属性的详细信息，请参阅 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)。|  
|PowerPivot:PowerPivot 数据刷新计时器作业被禁用。|否|否|SharePoint 2013<br /><br /> SharePoint 2010|检查计时器作业设置以便确认该计时器作业已启用。 如果未使用 PowerPivot 数据刷新功能，可以忽略此规则。 有关详细信息，请参阅[使用 SharePoint 2010 的 PowerPivot 数据刷新](../powerpivot-data-refresh-with-sharepoint-2010.md)。|  
|PowerPivot:管理 SQL Server 配置管理器的 SQL Server Analysis Services (PowerPivot) 服务帐户信息是不同于管理中心管理的帐户信息。|否|否|SharePoint 2010|此规则检查 SQL Server 配置管理器中的服务帐户信息是否与同一 Analysis Services 实例的管理中心中的托管帐户信息相同。 如果帐户不同，会将一个条目添加到“问题和解决方法”报告中，以便您可以将 SQL Server 配置管理器中的服务帐户信息改回管理中心中指定的帐户。 不支持使用 SQL Server 配置管理器在 PowerPivot for SharePoint 安装中更改服务帐户用户名或密码。 使用管理中心将允许使用 SharePoint 中的托管帐户功能。 更重要的是，如果您的场包含多个 PowerPivot for SharePoint 服务器，具有不一致的服务帐户设置可能破坏具有不正确服务信息的服务器上的处理和查询操作。<br /><br /> 在单个服务器上，触发此规则时 PowerPivot 工作簿将暂时运行，但是建议您尽快解决问题。 使用管理中心中指定的帐户信息更新数据库和文件系统权限。|  
|PowerPivot:部署的场解决方案不是最新的。|否|是|SharePoint 2010|PowerPivot for SharePoint 安装使用场级解决方案和 Web 应用程序级解决方案来安装其功能。 此规则指示场解决方案当前不与版本、服务器或 Web 解决方案相关。 很可能这是服务器部署问题。 要解决此问题，请考虑运行 SQL Server 安装程序来修复场中的某个 PowerPivot for SharePoint 安装。 PowerPivot for SharePoint 安装中的解决方案的详细信息，请参阅[部署 PowerPivot 解决方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)。|  
|PowerPivot:总体 CPU 使用率是太高。|是|否|SharePoint 2010|此规则报告系统级别的 CPU 使用情况。 整体 CPU 使用率进行监视，因为 PowerPivot 系统服务使用它作为服务器运行状况的度量值基于运行状况的负载均衡在多个 PowerPivot for SharePoint 服务器场中。 考虑向场中添加另一个应用程序服务器，并将 CPU 密集型应用程序移到该服务器。|  
|PowerPivot:Analysis Services 没有足够的 CPU 资源来执行请求的操作。|是|否|SharePoint 2010|可用于 Analysis Services 进程 (msmdsrv.exe) 的 CPU 资源对于此服务器上的活动级别不足。 考虑向场中添加另一个 PowerPivot for SharePoint 服务器。 有关详细信息，请参阅[部署核对清单：通过向 SharePoint 2010 场添加 PowerPivot 服务器来进行扩展](../../sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)。|  
|PowerPivot:Analysis Services 没有足够的内存来执行请求的操作。|否|否|SharePoint 2010|Analysis Services 仅剩下 5% 的可用内存时触发此规则。 在 SharePoint 应用程序服务器上，SQL Server Analysis Services 实例应该始终保留总是不会使用的少量内存。 因为对于其主要操作而言服务器是受到内存限制的，所以，令服务器在运行时永远不会达到其上限可使服务器保持最佳运行状态。<br /><br /> 默认情况下，在可用内存降到 5% 时出现内存不足警告。 您可以通过在 Analysis Services 实例上调整设置，将此值增大或减小。 有关详细信息，请参阅[PowerPivot 运行状况规则-配置](configure-power-pivot-health-rules.md)。<br /><br /> 该 5% 的未使用内存是按占分配给 Analysis Services 的内存的百分比计算的。 例如，如果您具有 200 GB 的总内存，并且 Analysis Services 被分配了总内存的 80%（也就是 160 GB），则 5% 的未使用内存为 160 GB 的 5%（也就是 8 GB）。|  
|PowerPivot:连接数目较高指示应部署更多服务器以处理当前负载。|是|否|SharePoint 2010|默认情况下，当非重复用户连接超过 100 时触发此运行状况规则。 此默认值是任意的（它不基于您服务器的硬件规范或用户活动），因此，您可以根据您环境中的服务器容量和用户活动来增大或减小该值。 有关详细信息，请参阅[PowerPivot 运行状况规则-配置](configure-power-pivot-health-rules.md)。|  
|PowerPivot:加载事件与连接比过高。|是|否|SharePoint 2013<br /><br /> SharePoint 2010|默认情况下，当在整个数据收集期内（默认为 4 小时）负载事件与连接事件的百分比超过 50% 时触发此运行状况规则。 此比例高表示到唯一工作簿的连接数目很大或缓存减少设置不当（工作簿快速卸载并从系统中删除，同时对该数据的请求仍有效）。 为了避免计入假正结果，在计算此比例前在 4 小时内至少必须有 20 个连接。 可以基于不同比例设置此运行状况规则。 有关详细信息，请参阅[PowerPivot 运行状况规则-配置](configure-power-pivot-health-rules.md)。 有关配置缓存的详细信息，请参阅[配置的磁盘空间使用情况&#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)。|  
|PowerPivot:表明程序崩溃的日志目录中找到了一个或多个小型转储文件。|否|否|SharePoint 2013<br /><br /> SharePoint 2010|在程序崩溃期间生成小型转储文件，以捕获有关在崩溃前那一刻 PowerPivot 服务应用程序状态的信息。 此信息可以发送给 Microsoft 用于故障排除。 在服务器上检测到 .dmp 文件时触发此规则。 此规则提供到该文件的链接，该文件位于 PowerPivot for SharePoint 实例的 \OLAP\Log 文件夹中。 请注意不能使用文本编辑器查看该文件的内容。 查看小型转储文件需要下载并安装单独的调试工具。 有关详细信息，请参阅 [Debugging Tools for Windows](/windows-hardware/drivers/debugger/)（Windows 调试工具）。|  
|PowerPivot:磁盘空间不足缓存 PowerPivot 数据的驱动器上。|是|否|SharePoint 2010|默认情况下，在备份文件夹所在的磁盘驱动器上，如果磁盘空间低于 5%，将触发此运行状况规则。 有关设置此百分比的详细信息，请参阅[PowerPivot 运行状况规则-配置](configure-power-pivot-health-rules.md)。 有关磁盘使用情况的详细信息，请参阅[配置的磁盘空间使用情况&#40;PowerPivot for SharePoint&#41;](configure-disk-space-usage-power-pivot-for-sharepoint.md)。|  
|PowerPivot:使用情况数据未按照预期频率进行更新。|是|否|SharePoint 2013<br /><br /> SharePoint 2010|PowerPivot for SharePoint 使用内置的使用情况数据收集系统来收集与连接、数据刷新和查询响应次数有关的度量。 它在 PowerPivot 服务应用程序数据库中存储此使用情况数据，而这又更新了向 PowerPivot 管理面板中的报表提供数据的 PowerPivot 工作簿 (PowerPivot Management Data.xlsx)。 此规则指示使用情况数据未以足够频率向 PowerPivot Management Data.xlsx 文件移动。 此规则使用 .xlsx 文件上的时间戳作为文件更新的证据。 如果使用情况数据收集系统中存在影响数据准确性的其他问题，此规则无法检测到。 要消除此错误，请检查计时器作业以便确认它们正在运行。 有关使用情况数据收集的详细信息，请参阅[配置使用情况数据收集的&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。|  
|PowerPivot:Midtier 进程帐户应该对所有关联的 spwebapplications 都具有完全读取权限。|否|是|SharePoint 2013<br /><br /> SharePoint 2010|PowerPivot 服务应用程序标识必须具有**完全读取**权限，才能访问 SharePoint 内容数据库代表对文档具有仅查看权限的用户。 若要确定哪个帐户用作 PowerPivot 服务应用程序标识，打开**服务帐户配置**管理中心页。 很可能该服务应用程序在 **“SharePoint Web 服务系统”** 服务应用程序池或专用应用程序池中运行。 虽然此规则提供了一个自动修复选项，则会更好的结果，如果你手动授予权限通过执行以下操作：<br /><br /> 1) 在管理中心中，单击“管理 Web 应用程序”。 <br /><br /> 2) 选择一个网站，然后单击“用户策略”。 <br /><br /> 3) 单击“添加用户”。 <br /><br /> 4) 选择“(所有区域)”，然后单击“下一步”。 <br /><br /> 5） 在用户中，输入 PowerPivot 服务应用程序标识，并单击**完全读取**复选框。 单击 **“完成”** 。<br /><br /> 6) 确认修复。 在“监视”中，单击 **“审核规则定义”** 。 找到 PowerPivot 规则，然后将其打开。 单击 **“立即运行”** 。 返回到 **“查看问题和解决方法”** ，确认该规则不会再出现。|  
|PowerPivot:已禁用辅助登录服务 (seclogon)|否|否|SharePoint 2013<br /><br /> SharePoint 2010|辅助登录服务用于在 PowerPivot 库中生成 PowerPivot 工作簿的缩略图。 默认情况下，辅助登录服务设置为手动启动。 如果禁用该服务，则缩略图的生成将失败。 此外，ULS 日志将包含以下错误："错误 1058年的根源这一事实 '辅助登录' 已禁用的 Windows 服务时可以有"<br /><br /> 若要查看服务配置，请使用服务控制台应用程序查找辅助登录并且将其 **“启动类型”** 更改为 **“手动”** 。 如果您不能启用该服务，则您的组织可能具有禁用该服务的组策略。 请向您的管理员核实以便确认是否属于这一情况。<br /><br /> 在启用该服务后，缩略图或快照图像将会随着时间的推移而刷新。 或者，您可以通过重新启动该服务，并且在打开后再重新保存特定报表的属性页，强制进行刷新。 有关详细信息，请参阅[如何使用 PowerPivot 库](https://go.microsoft.com/fwlink/?LinkId=246462)。|  
|PowerPivot:ADOMD.NET 未安装在独立配置为进行集中管理的 WFE 上|否|否|SharePoint 2013<br /><br /> SharePoint 2010|ADOMD.NET 是支持与 Analysis Services 数据库连接的 Analysis Services 客户端库。 在 PowerPivot for SharePoint 的部署中，ADOMD.NET 在管理中心的 PowerPivot 管理面板中提供对内置报表的访问。 内置报表实际上是包含嵌入的 Analysis Services 数据的 PowerPivot 工作簿。 该管理面板使用 ADOMD.NET 将连接请求发送到加载工作簿所含数据的服务器。<br /><br /> 在包含运行于独立 Web 前端服务器上的管理中心的拓扑结构上，如果您要在管理面板中查看这些报表，则必须手动安装 ADOMD.NET。 有关详细信息，请参阅 [在运行管理中心的 Web 前端服务器上安装 ADOMD.NET](../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)。|  
  
  
