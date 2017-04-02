---
title: "Claims to Windows Token Service (c2WTS) 和 Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "c2wts.exe.config"
  - "SharePoint 模式"
  - "C2WTS"
  - "WSS_WPG"
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Claims to Windows Token Service (c2WTS) 和 Reporting Services
  如果你想要对 SharePoint 场外的数据源使用 Windows 身份验证，需要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式下使用 SharePoint Claims to Windows Token Service (c2WTS)。 即使用户使用 Windows 身份验证访问数据源，上述要求也是成立的。其原因在于，Web 前端 (WFE) 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务之间的通信将始终是声明身份验证。  
  
 即使你的数据源与共享服务位于相同的计算机上，也需要 c2WTS。 但在此方案中，不需要约束委派。  
  
 c2WTS 创建的令牌将仅用于约束委派（对特定服务的约束）以及配置选项“使用任何身份验证协议”。 如前所述，如果您的数据源与共享服务位于同一台计算机上，则不需要约束委派。  
  
 如果您的环境将使用 Kerberos 约束委派，则 SharePoint 服务器服务和外部数据源需要位于同一 Windows 域中。 依赖于 Claims to Windows Token Service (c2WTS) 的所有服务都必须使用 Kerberos **约束**委派，以便允许 c2WTS 使用 Kerberos 协议转换将声明转换为 Windows 凭据。 这些规定适用于所有 SharePoint 共享服务。 有关详细信息，请参阅[在 SharePoint 2013 中规划 Kerberos 身份验证](http://technet.microsoft.com/library/ee806870.aspx)。  
  
 本主题将概述此过程。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2016 | SharePoint 2013|  
  
## 先决条件  
  
> [!NOTE]  
>  请注意，某些配置步骤可能会更改，或者在某些场拓扑中不适用。 例如，单服务器安装并不支持 Windows Identity Foundation c2WTS 服务，因此，在该场配置中不可能实现 Claims to Windows Token 委派方案。 

> [!IMPORTANT] 如果将 Power View 与 Power Pivot 工作簿配合工作，将需要为 [Office Online 服务器概述](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx)进行其他配置。 有关详细信息，请参阅以下白皮书。 
>
> - [在 SharePoint 2016 中部署 SQL Server 2016 PowerPivot 和 Power View](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
> 
> - [在多层 SharePoint 2016 场中部署 SQL Server 2016 PowerPivot 和 Power View](../../analysis-services/instances/install-windows/deploy powerpivot and power view - multi-tier sharepoint 2016 farm.md)
  
### 配置 c2WTS 所需的基本步骤  
  
1.  配置 c2WTS 服务帐户。 将该服务帐户添加到运行 c2WTS 的每个应用程序服务器上的本地管理员组。 此外，确认该帐户具有以下本地安全策略权限：  
  
    -   以操作系统方式操作  
  
    -   在身份验证后模拟客户端  
  
    -   作为服务登录  
  
2.  配置 c2WTS 服务帐户的委派。 该帐户需要具有协议转换的约束委派，并且需要相应权限以便委派给需要与之通信的服务（即 SQL Server 引擎、SQL Server Analysis Services）。 若要配置委派，你可以使用 Active Directory 用户和计算机管理单元。  

    > [!IMPORTANT] 无论在委派选项卡上为 C2WTS 服务帐户配置何种设置，都需要与 Reporting Services 服务帐户相匹配。 例如，如果你允许将 C2WTS 服务帐户委派给 SQL 服务，则需要对 Reporting Services 服务帐户执行相同操作。
  
    1.  右键单击各服务帐户并且打开“属性”对话框。 在该对话框中，单击 **“委派”** 选项卡。  
  
        > [!NOTE]  
        >  请注意，只有在对象具有分配给它的服务主体名 (SPN) 的情况下，“委派”选项卡才可见。 c2WTS 不要求在 c2WTS 帐户上具有 SPN；但如果没有 SPN，“委派”选项卡将不可见。 配置约束委派的另一个方法是使用 **ADSIEdit**之类的实用工具。  
  
    2.  “委派”选项卡上的主要配置选项如下：  
  
        -   选择“仅信任此用户对指定服务的委派”  
  
        -   选择“使用任何身份验证协议”  

    3. 选择“添加”以添加要委派的服务。
    
    4. 选择*“用户或计算机...”并输入托管服务的帐户。例如，如果在名为 *sqlservice * 的帐户下运行 SQL Server，则输入 `sqlservice`。
    
    5. 选择服务列表。 将显示该帐户可用的 SPN。 如果在该帐户上没有看到列出的服务，则它可能已丢失或放置在不同的帐户上。 可以使用 SetSPN 实用工具调整 SPN。
    
    6. 选择“确定”以退出对话框。
  
3.  配置 c2WTS“AllowedCallers”  
  
     c2WTS 需要在配置文件 **c2WTShost.exe.config**中显式列出的“调用方”标识。 c2WTS 不接受来自系统中所有验证了身份的用户的请求，除非配置为这样做。 在此情况下，“调用方”是 WSS_WPG Windows 组。 c2WTShost.exe.confi 文件保存在以下位置：  
     
     > [!NOTE] 在 SharePoint 管理中心为 C2WTS 服务更改服务帐户，会将该帐户添加到 WSS_WPG 组中。
  
     **\Program Files\Windows Identity Foundation\v3.5\c2WTShost.exe.config**  
  
     下面是该配置文件的示例：  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```    
4.  启动 SharePoint“Claims to Windows Token Service”：通过 SharePoint 管理中心上的 **“管理服务器上的服务”** 页启动 Claims to Windows Token Service。 应在将执行操作的服务器上启动该服务。 例如，如果你有一个作为 WFE 的服务器，并且有另一个作为应用程序服务器的服务器（该服务器具有正在运行的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务），则只需启动该应用程序服务器上的 c2WTS。 在 WFE 上不需要 c2WTS。  
  
## 另请参阅  
 [Claims to Windows Token Service (c2WTS) 概述](http://msdn.microsoft.com/library/ee517278.aspx)   
 [在 SharePoint 2013 中规划 Kerberos 身份验证](http://technet.microsoft.com/library/ee806870.aspx)  
  
  