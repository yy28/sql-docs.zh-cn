---
title: "配置 Analysis Services 和 Kerberos 约束委派 (KCD) |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0006e143-d3ba-4d10-a415-e42c45e2bb0a
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c13b9095224d1c33e09c9513121e46483da05c0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>配置 Analysis Services 和 Kerberos 约束委派 (KCD)
  Kerberos 约束委派 (KCD) 是一种身份验证协议，你可以使用 Windows 身份验证进行配置，使其在整个环境的服务之间委派客户端凭据。 KCD 需要附加基础结构（例如域控制器）和你环境中的其他配置。 在某些通过 SharePoint 2016 涉及 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 数据的方案中，要求使用 KCD。 在 SharePoint 2016 中，Excel Services 已从 SharePoint 场移出到单独的新服务器，即 **Office Online Server**。 由于 Office Online Server 是独立的服务器，因此在两个典型的跃点方案中更加需要委派客户端凭据的方法。  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
## <a name="overview"></a>概述  
 KCD 可以使一个帐户模拟另一个帐户，从而提供对资源的访问权限。 模拟帐户可以是分配给 Web 应用程序的服务帐户或 Web 服务器的计算机帐户，被模拟帐户可以是需要资源访问权限的用户帐户。 由于 KCD 在服务层进行操作，因此可通过模拟帐户对服务器上的选定服务授予访问权限，而同一服务器上的其他服务或其他服务器上的服务将被拒绝访问。  
  
 本主题中的各部分考察需要使用 KCD 的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 的常见方案，并提供了一个服务器部署示例，该示例中高度概述了需要安装和配置的项。 请参阅 [更多信息和社区内容](#bkmk_moreinfo) 部分，了解有关所涉及技术（例如域控制器和 KCD）的更多详细信息。  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>方案 1：工作簿作数据源 (WDS)。  
 ![请参阅 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "请参阅 1") Office Online Server 打开一个 Excel 工作簿和![请参阅 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "请参阅 2")检测到另一个工作簿的数据连接。 Office Online Server 将请求发送到[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]重定向程序服务![请参阅 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "请参阅 3")若要打开第二个工作簿和数据![，请参阅 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "，请参阅 4").  
  
 在此方案中，需要将用户凭据从 Office Online Server 委派给 SharePoint 中的 SharePoint [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 重定向程序服务。  
  
 ![作为数据源的工作簿](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "作为数据源的工作簿")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>方案 2：Analysis Services 表格模型链接到 Excel 工作簿  
 Analysis Services 表格模型![请参阅 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "请参阅 1")链接到 Excel 工作簿，其中包含 Power Pivot 模型。 在此方案中，当 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 加载表格模型时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将检测指向该工作簿的链接。 在处理模型时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 会将查询请求发送到 SharePoint，以加载工作簿。 在此方案中， **无需** 将客户端凭据从 Analysis Services 委派到 SharePoint，但是客户端应用程序可以覆盖外部绑定中的数据源信息。 如果外部绑定请求指定模拟当前用户，则必须委派用户凭据，这需要在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 和 SharePoint 之间配置 KCD。  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>使用 Office Online Server 和 Analysis Services 的 KCD 部署示例  
 本部分介绍了使用四台计算机的部署示例。 以下部分总结了每台计算机的主要安装和配置步骤。 在开始部署之前，建议为计算机安装最新的操作系统修补程序并了解计算机名，因为某些配置步骤中将需要使用它们。  
  
-   域控制器  
  
-   SQL Server 数据库引擎和处于 Power Pivot 模式的 Analysis Services。 数据库引擎的实例将用于 SharePoint 内容数据库。  
  
-   SharePoint Server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>域控制器  
 下面是关于域控制器 (DC) 的安装内容摘要。  
  
-   **角色：** Active Directory 域服务。 有关概述，请参阅 [在 Windows Server 2012 中配置 Active Directory (AD DS)](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)。  
  
-   **角色：** DNS 服务器  
  
-   **功能：** .NET Framework 3.5 功能/.NET Framework 3.5  
  
-   **功能：** 远程服务器管理工具/角色管理工具  
  
-   配置 Active Directory 以创建新的林并将计算机加入域。 在尝试将其他计算机添加到专用域之前，需要将客户端计算机 DNS 配置为 DC 的 IP 地址。 在 DC 计算机上，运行 `ipconfig /all` 获取 IPv4 和 IPv6 地址以便进行下一步。  
  
-   建议同时配置 IPv4 和 IPv6 地址。 可以在 Windows 控制面板中执行此操作：  
  
    1.  单击“网络和共享中心”   
  
    2.  单击你的以太网连接  
  
    3.  单击“属性”   
  
    4.  单击“Internet 协议版本 6 (TCP/IPv6)”   
  
    5.  单击“属性”   
  
    6.  单击“使用下面的 DNS 服务器地址”   
  
    7.  通过 ipconfig 命令键入 IP 地址。  
  
    8.  单击“高级”  按钮，再单击“DNS”  选项卡并验证 DNS 后缀是否正确。  
  
    9. 单击“追加这些 DNS 后缀”   
  
    10. 对 IPv4 重复以上步骤。  
  
-   **注意：** 可通过系统设置从 Windows 控制面板将计算机加入域。 有关详细信息，请参阅 [How To Join Windows Server 2012 to a Domain（如何将 Windows Server 2012 加入域）](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)。  
  
 ![在 powerpivot 模式下的 ssas 服务器](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "正在 powerpivot 模式下的 ssas 服务器")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>2016 SQL Server 数据库引擎和处于 Power Pivot 模式的 Analysis Services  
 下面是要关安装在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 计算机上的内容的摘要。  
  
 ![请注意](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")中[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]安装向导中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]在 Power Pivot 模式下安装作为功能选择工作流的一部分。  
  
1.  运行 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 安装向导，然后从功能选择页单击数据库引擎、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]和管理工具。 稍后通过安装向导进行安装时，可以为 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]模式。  
  
2.  对于实例配置，请配置名为“POWERPIVOT”的实例。  
  
3.  在 Analysis Services 配置页上，配置处于 **Power Pivot** 模式的 Analysis Services 服务器，并将 Office Online Server 的 **计算机名** 添加到 Analysis Services 服务器管理员列表中。 有关详细信息，请参阅 [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)。  
  
4.  请注意，默认情况下，搜索中不包括“计算机”对象类型。 单击![单击要添加计算机帐户对象](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "单击要添加计算机帐户对象")以添加计算机对象。  
  
     ![将计算机帐户添加为 ssas 管理员](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "将计算机帐户添加为 ssas 管理员")  
  
5.  为 Analysis Services 实例创建服务主体名称 (SPN)。  
  
     以下是有用的 SPN 命令：  
  
    -   为运行所需服务的特定帐户名列出 SPN： `SetSPN -l <account-name>`  
  
    -   为运行所需服务的帐户名设置 SPN： `SetSPN -a <SPN> <account-name>`  
  
    -   从运行所需服务的特定帐户名删除 SPN： `SetSPN -D <SPN> <account-name>`  
  
    -   搜索重复的 SPN： `SetSPN -X`  
  
     PowerPivot 实例的 SPN 格式如下：  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     其中 FQDN 和 NetBIOS 名称是该实例所在计算机的名称。 这些 SPN 将放置在正用于服务帐户的域帐户之上。  如果使用网络服务、本地系统或服务 ID，建议将 SPN 放置在域计算机帐户之上。  如果使用域用户帐户，请将 SPN 直接置于该帐户之上。  
  
6.  在 Analysis Services 计算机上为 SQL Browser 服务创建 SPN。  
  
     [了解更多信息](https://support.microsoft.com/en-us/kb/950599)  
  
7.  在 Analysis Services 服务帐户中为你将从其中刷新的任何外部源（例如 SQL Server 或 Excel 文件）**配置约束委派** 设置。 在 Analysis Services 服务帐户中，确保设置以下内容：  
  
     **注意：** 如果在“Active Directory 用户和计算机”中看不到该帐户的委派选项卡，这是由于该帐户上没有任何 SPN 而导致的。  你可以添加一个虚设的 SPN 使其显示出来，例如 `my/spn`。  
  
     “仅信任此用户作为指定服务的委派” 和“使用任何身份验证协议” 。  
  
     这称为约束委派，并且为必需，因为 Windows 令牌将生成自“声明为 Windows 令牌服务(C2WTS)”，而改服务需要具有协议转换的约束委派。  
  
     ![Analysis Services-约束委派](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services-约束委派")  
  
     此外，还需要添加将委派到的服务。 这将因你的环境而有所不同。  
  
### <a name="office-online-server"></a>Office Online Server  
  
1.  安装 Office Online Server  
  
2.  **配置 Office Online Server** 以连接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器。 请注意，Office Online Server 计算机帐户在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器上必须是管理员帐户。 在本主题上一部分（安装 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服务器）中已完成这种配置。  
  
    1.  在 Office Online Server 上，使用管理员权限打开 PowerShell 窗口并运行以下命令  
  
    2.  `New-OfficeWebAppsExcelBIServer –ServerId <AS instance name>`  
  
    3.  示例： `New-OfficeWebAppsExcelBIServer –ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **配置 Active Directory** 以便允许Office Online Server 计算机帐户模拟用户的 SharePoint 服务帐户。 在运行 SharePoint Web Services 的应用程序池的主体上，在 Office Online Server 上设置委派属性：本部分中的 PowerShell 命令需要 Active Directory (AD) PowerShell 对象。  
  
    1.  获取 Office Online Server 的 Active Directory 标识  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         查看“任务管理器”/“详细信息”/“w3wp.exe 的用户名”即可找到此主体名称。 例如“svcSharePoint”  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  验证属性是否设置正确  
  
    3.  ```  
        Get-ADUser svcSharePoint –Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  将 Office Online Server 帐户的**约束委派** 设置配置为 Analysis Services Power Pivot 实例。 此实例应为 Office Online Server 运行于的计算机帐户。 在 Office Online Service 帐户中，确保设置以下内容。  
  
     **注意：** 如果在“Active Directory 用户和计算机”中看不到该帐户的委派选项卡，这是由于该帐户上没有任何 SPN 而导致的。  你可以添加一个虚设的 SPN 使其显示出来，例如 `my/spn`。  
  
     “仅信任此用户作为指定服务的委派” 和“使用任何身份验证协议” 。  
  
     这称为约束委派，并且为必需，因为 Windows 令牌将生成自“声明为 Windows 令牌服务(C2WTS)”，而改服务需要具有协议转换的约束委派。  然后允许向上面创建的 MSOLAPSvc.3 和 MSOLAPDisco.3 SPNs 进行委派。  
  
5.  安装声明为 Windows 令牌服务 (C2WTS) **这是方案 1 的必需操作**。 有关详细信息，请参阅 [Claims to Windows Token Service (c2WTS) 概述](https://msdn.microsoft.com/library/ee517278.aspx)。  
  
6.  在 C2WTS 服务帐户上**配置约束委派** 设置。  此处的设置应与步骤 4 中的操作一致。  
  
 ![sharepoint server](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "sharepoint 服务器")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 以下是关于 SharePoint Server 安装的摘要。  
  
1.  运行 SharePoint 必备安装程序  
  
2.  运行 SharePoint 安装，并选择“单个服务器场”  安装角色。  
  
3.  运行 PowerPivot for SharePoint 加载项 (spPowerPivot16.msi)。 有关详细信息，请参阅[安装或卸载 Power Pivot for SharePoint 外接程序 (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  运行 PowerPivot 配置向导。 请参阅 [Power Pivot Configuration Tools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
5.  将 SharePoint 连接到 Office Online Server。    ??Configure_xlwac_on_SPO.ps1 ??  
  
6.  为 Kerberos 配置 SharePoint 身份验证提供程序。 **这是方案 1 的必需操作**。 有关详细信息，请参阅 [在 SharePoint 2013 中规划 Kerberos 身份验证](https://technet.microsoft.com/library/ee806870.aspx)。  
  
##  <a name="bkmk_moreinfo"></a> 更多信息和社区内容  
 [一个忙碌的管理员眼中的 Kerberos](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [了解 Kerberos 双跃点](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [.Net 与 SharePoint 面面观](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [基于资源的 Kerberos 约束委派](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [KERBEROS 入门 - 视频](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft® Kerberos Configuration Manager for SQL Server®](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  

