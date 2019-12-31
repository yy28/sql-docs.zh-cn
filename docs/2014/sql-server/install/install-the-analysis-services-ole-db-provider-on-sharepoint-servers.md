---
title: 在 SharePoint 服务器上安装 Analysis Services OLE DB Provider |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2c62daf9-1f2d-4508-a497-af62360ee859
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f8dcec71f8b9c90df9f30aa5bfb972fef28fbcd7
ms.sourcegitcommit: 381595e990f2294dbf324ef31071e2dd2318b8dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2019
ms.locfileid: "74200448"
---
# <a name="install-the-analysis-services-ole-db-provider-on-sharepoint-servers"></a>在 SharePoint 服务器上安装 Analysis Services OLE DB 访问接口
  Microsoft OLE DB Provider for Analysis Services (MSOLAP) 是客户端应用程序用来与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据进行交互的接口。 在包含 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]的 SharePoint 环境中，此访问接口用于处理对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的连接请求。  
  
 此数据访问接口包含在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装包 (spPowerPivot.msi) 中，但可能需要手动安装。 有两个原因您可能需要在 SharePoint 服务器上手动安装客户端库或数据访问接口。  
  
-   **启用向后兼容性**。 
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 工作簿在连接字符串中指定 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的 Analysis Services OLE DB 访问接口。 因此，计算机上必须存在此访问接口版本，请求才能成功。  
  
-   **在专用 Excel Services 实例上启用数据访问**。 如果 SharePoint 场包含的 Excel Services 位于未安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]的服务器上，则可使用 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 安装包安装访问接口的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 版本和其他客户端连接组件。  
  
    > [!NOTE]  
    >  这些方案并不相互冲突。 如果在包含运行 Excel Services 的应用程序服务器的场上承载多个工作簿版本而没有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 实例，您需要在每个 Excel Services 计算机上同时安装数据访问接口的较旧版本和较新版本。  
  
  
##  <a name="bkmk_vers"></a>支持 PowerPivot 数据访问的 OLE DB 提供程序的版本  
 SharePoint 场可能会包含 Analysis Services OLE DB 访问接口的多个版本，其中包括不支持 PowerPivot 数据访问的较早版本。  
  
 默认情况下，SharePoint 2010 安装 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本的访问接口。 虽然标识为 MSOLAP.4（与用于 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]的版本号相同），但此版本不能用于 PowerPivot 数据访问。 要确保连接成功，您必须拥有 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的访问接口。  
  
 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之后的 OLE DB 访问接口版本包括对 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据结构的传输和连接支持。 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿使用此访问接口的较新版本从场中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务器请求查询处理。 若要获取更新后的版本，可以通过“SQL Server 功能包”页下载并安装它。  
  
 下表对有效版本进行了说明：  
  
|产品版本|文件版本|适用于：|  
|---------------------|------------------|----------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|在文件系统中为 MSOLAP100.dll<br /><br /> 在 Excel 连接字符串中为 MSOLAP.4<br /><br /> 在文件版本详细信息中为 10.50.1600 或更高版本|用于使用 PowerPivot for Excel 的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本创建的数据模型。|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|在文件系统中为 MSOLAP110.dll<br /><br /> 在 Excel 连接字符串中为 MSOLAP.5<br /><br /> 在文件版本详细信息中为 11.0.0000 或更高版本|用于使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] for Excel 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 版本创建的数据模型。|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|在文件系统中为 MSOLAP120.dll<br /><br /> 在文件版本详细信息中为 12.0.20000 或更高版本|用于除 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型以外的其他数据模型。|  
  
  
##  <a name="bkmk_why"></a>为什么需要安装 OLE DB 提供程序  
 有两种情况需要在场中的服务器上手动安装 OLE DB 访问接口。  
  
 **最常见的情况**是，在场中的文档库中[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]保存了较旧和较新版本的工作簿。 如果你的组织中的分析人员使用的是 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel，并已将这些工作簿保存到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装，则较旧版本的工作簿将无法使用。 它的连接字符串将引用旧版本的访问接口，除非您安装该版本，否则不会在服务器上。 安装两个版本将可以对较旧版本和较新版本的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中创建的 PowerPivot 工作簿启用数据访问。 
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安装程序不会安装 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的访问接口，因此必须手动安装此版本（如果使用先前版本的工作簿）。  
  
 **第二种情况**是： SharePoint 场中的某个服务器运行的是 Excel Services，而不[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]是。 在这种情况下，必须将运行 Excel Services 的应用程序服务器手动更新为使用访问接口的较新版本。 这对于连接到 PowerPivot for SharePoint 实例是必需的。 如果 Excel Services 使用较旧版本的访问接口，连接请求将失败。 请注意，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序或 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装包 (spPowerPivot.msi) 安装访问接口，才能确保安装支持 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 所需的所有组件。  
  
  
##  <a name="bkmk_sql11"></a>使用 SQL Server 安装程序在 Excel Services 服务器上安装 SQL Server 2012 OLE DB 提供程序  
 使用以下指令将 OLE DB 访问接口和其他客户端连接组件添加到尚未安装它们的 SharePoint 服务器（例如运行 Excel Services 但在同一硬件上没有安装 PowerPivot for SharePoint 的应用程序服务器）。  
  
 使用这些指令安装当前的 Analysis Services OLE DB 访问接口并将 **Microsoft.AnalysisServices.Xmla.dll** 添加到全局程序集。  
  
#### <a name="run-sql-server-setup-and-install-the-client-connectivity-tools"></a>运行 SQL Server 安装程序并安装客户端连接工具  
  
1.  在承载 Excel Services 的应用程序服务器上，运行 SQL Server 安装程序。  
  
2.  在“安装”页上，选择 **“全新 SQL Server 独立安装或向现有安装添加功能”**。  
  
3.  在“安装类型”页上，选择 **“执行 SQL Server 2012 的全新安装”**。  
  
4.  在“设置角色”页上，选择 **“SQL Server 功能安装”**。  
  
5.  在 **“功能选择”** 页中，单击 **“客户端工具连接”**。 此选项将安装 **Microsoft.AnalysisServices.Xmla.dll**  
  
     不要选择任何其他功能。  
  
6.  单击 **“下一步”** 完成向导，然后单击 **“安装”** 运行安装程序。  
  
7.  如果有运行 Excel Services 的其他服务器且未在其上安装 PowerPivot for SharePoint，请重复上述步骤。  
  
#### <a name="verify-msolap5-is-a-trusted-provider"></a>验证 MSOLAP.5 是受信任的访问接口。  
  
1.  在“管理中心”中，单击 **“管理服务应用程序”**，然后单击 Excel Services 服务应用程序。  
  
2.  单击 **“受信任的数据访问接口”**。  
  
3.  验证 MSOLAP.5 显示在列表中。 根据您配置 PowerPivot for SharePoint 的不同方式，MSOLAP.5 可能已受信任。 如果您使用了 PowerPivot 配置工具但是之后从任务列表中排除了此操作，MSOLAP.5 将不被 Excel Services 信任，现在需要手动添加。  
  
4.  如果未列出 MSOLAP，请单击 **“添加受信任的数据访问接口”**。  
  
5.  在“访问接口 ID”中，键入 `MSOLAP.5`。  
  
6.  对于“访问接口类型”，请确保选择 OLE DB。  
  
7.  在“访问接口说明”中，键入 **Microsoft OLE DB Provider for OLAP Services 11.0**。  
  
#### <a name="verify-installation"></a>验证安装  
  
1.  转到 Program files\Microsoft Analysis Services\AS OLEDB\110。  
  
2.  右键单击 msolap110.dll，然后选择“ **属性**”。  
  
3.  单击 **“详细信息”**。  
  
4.  查看文件版本信息。 版本应包含11.00。\<buildnumber>。  
  
5.  在 Windows\assembly 文件夹中，验证 Microsoft.AnalysisServices.Xmla.dll 版本 11.0.0.0 已列出。  
  
  
##  <a name="bkmk_install2012_from_sppowerpivot_msi"></a>使用 PowerPivot for SharePoint 安装包（Sppowerpivot.msi）安装 SQL Server 2012 OLE DB 提供程序  
 使用 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 安装包 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] (spPowerPivot.msi) **在 Excel Services 服务器上安装**OLE DB 访问接口。  
  
#### <a name="download-the-msolap5-provider-from-the-includesssql11sp1includessssql11sp1-mdmd-feature-pack"></a>从 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 功能包下载 MSOLAP.5 访问接口。  
  
1.  浏览至 [Microsoft® SQL Server® 2012 SP1 功能包](https://www.microsoft.com/download/details.aspx?id=35580)  
  
2.  单击 **“安装说明”**。  
  
3.  请参阅 "Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1" 一节。 下载该文件并开始安装。  
  
4.  在 **“功能选择”** 页，选择 **“用于 SQL Server 的 Analysis Services OLE DB 访问接口”**。 取消选择其他组件并完成安装。 有关 Sppowerpivot.msi 的详细信息，请参阅[&#40;SharePoint 2013&#41;中安装或卸载 PowerPivot for SharePoint 外接程序](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)。  
  
5.  将 MSOLAP.5 注册为 SharePoint Excel Services 中的受信任数据访问接口。 有关详细信息，请参阅 [将 MSOLAP.5 添加为 Excel Services 中的受信任数据访问接口](https://technet.microsoft.com/library/hh758436.aspx)。  
  
  
##  <a name="bkmk_kj"></a>安装 SQL Server 2008 R2 OLE DB 提供程序以承载早期版本的工作簿  
 使用以下说明来安装 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的 MSOLAP.4 访问接口并注册 Microsoft.AnalysisServices.ChannelTransport.dll 文件。 ChannelTransport 是 Analysis Services OLE DB 访问接口的子组件。 在使用 ChannelTransport 进行连接时， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的访问接口读取注册表。 注册此文件是安装后步骤，仅对于 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 服务器上 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 访问接口处理的连接是必需的。  
  
#### <a name="step-1-download-and-install-the-client-library"></a>步骤 1：下载并安装客户端库  
  
1.  在 [SQL Server 2008 R2 功能包页](https://www.microsoft.com/download/details.aspx?id=16978)上，查找 Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2008 R2。  
  
2.  下载 `SQLServer2008_ASOLEDB10.msi` 安装程序的 x64 包。 尽管文件名包含 SQLServer2008，但它是用于 SQL Server 2008 R2 版本的访问接口的正确文件。  
  
3.  在已安装 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]的计算机上，运行 .msi 以安装该库。  
  
4.  如果您在场中有仅运行 Excel Services 的其他服务器（而没有在同一服务器上的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] ），请重复以前的步骤以在 Excel Services 计算机上安装 2008 R2 版本的访问接口。  
  
#### <a name="step-2-register-the-microsoftanalysisserviceschanneltransportdll-file"></a>步骤 2：注册 Microsoft.AnalysisServices.ChannelTransport.dll 文件  
  
1.  使用 regasm.exe 实用工具注册该文件。 如果之前未运行 regasm，请将其父文件夹 C:\Windows\Microsoft.NET\Framework64\v4.0.30319\\添加到系统路径变量。  
  
2.  使用管理员权限打开命令提示符。  
  
3.  转至此文件夹 C:\Windows\assembly\GAC_MSIL\Microsoft.AnalysisServices.ChannelTransport\10.0.0.0__89845dcd8080cc91  
  
4.  输入以下命令：`regasm microsoft.analysisservices.channeltransport.dll`  
  
5.  在手动安装 2008 R2 版本的访问接口的所有计算机上重复以前的步骤。  
  
#### <a name="verify-installation"></a>验证安装  
  
1.  您现在应可以切片或筛选 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 工作簿。 如果发生错误，请验证您使用了 64 位版本的 regasm.exe 来注册文件。  
  
2.  此外，您可以检查文件版本。  
  
     转到  `C:\Program files\Microsoft Analysis Services\AS OLEDB\10` 。 右键单击 **msolap100.dll** 并选择 **“属性”**。 单击 **“详细信息”**。  
  
     查看文件版本信息。 版本应包含10.50。\<buildnumber>。  
  
  
## <a name="see-also"></a>另请参阅  
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
