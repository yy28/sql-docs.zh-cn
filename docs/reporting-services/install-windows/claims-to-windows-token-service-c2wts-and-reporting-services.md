---
title: "Claims to Windows Token Service (c2WTS) 和 Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 09/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: fcc2707cb5febc11d033e745a41fd15dbdbddb7c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) 和 Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

如果要在 [SQL Server Reporting Services 报表查看器 Web 部件](../report-server-sharepoint/deploy-report-viewer-web-part.md)中查看本机模式报表，需要 SharePoint Claims to Windows Token Service (C2WTS)。

如果要对 SharePoint 场外的数据源使用 Windows 身份验证，也需要在 SQL Server Reporting Services SharePoint 模式下使用 C2WTS。 即使您的数据源与共享服务位于相同的计算机上，也需要 C2WTS。 但在此方案中，不需要约束委派。

> [!NOTE]
> 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。

## <a name="report-viewer-web-part-configuration"></a>报表查看器 Web 部件配置

报表查看器 Web 部件可用于嵌入 SharePoint 站点中的 SQL Server Reporting Services 本机模式报表。 此 Web 部件可用于 SharePoint 2013 和 SharePoint 2016。 SharePoint 2013 和 SharePoint 2016 都使用声明身份验证。 SQL Server Reporting Services（本机模式）默认使用 Windows 身份验证。 因此，需要正确配置 C2WTS，以正确呈现报表。

## <a name="sharepoint-mode-integaration"></a>SharePoint 模式集成

**本节仅适用于 SQL Server 2016 Reporting Services 及更早版本。**

如果要对 SharePoint 场外的数据源使用 Windows 身份验证，需要在 SQL Server Reporting Services SharePoint 模式下使用 SharePoint Claims to Windows Token Service (C2WTS)。 即使用户使用 Windows 身份验证访问数据源，上述要求也是成立的。其原因在于，Web 前端 (WFE) 和 Reporting Services 共享服务之间的通信将始终是声明身份验证。

## <a name="steps-needed-to-configure-c2wts"></a>配置 c2WTS 所需的步骤

C2WTS 创建的令牌将仅用于约束委派（对特定服务的约束）以及配置选项“使用任何身份验证协议”。 如前所述，如果您的数据源与共享服务位于同一台计算机上，则不需要约束委派。

如果您的环境将使用 Kerberos 约束委派，则 SharePoint 服务器服务和外部数据源需要位于同一 Windows 域中。 依赖于 Claims to Windows Token Service (c2WTS) 的所有服务都必须使用 Kerberos **约束** 委派，以便允许 c2WTS 使用 Kerberos 协议转换将声明转换为 Windows 凭据。 这些规定适用于所有 SharePoint 共享服务。 有关详细信息，请参阅 [在 SharePoint 2013 中规划 Kerberos 身份验证](http://technet.microsoft.com/library/ee806870.aspx)。  

1. 配置 C2WTS 服务帐户。 将该服务帐户添加到将使用 C2WTS 的每个服务器上的本地管理员组。

    对于报表查看器 Web 部件，这是 Web 前端 (WFE) 服务器。 对于 SharePoint 集成模式，这是运行 Reporting Services 服务的应用程序服务器。

2. 配置 C2WTS 服务帐户的委派。

    该帐户需要具有协议转换的约束委派，并且需要相应权限以便委派给需要与之通信的服务（即 SQL Server 数据库引擎、SQL Server Analysis Services）。 要配置委派，可使用 Active Directory 用户和计算机管理单元，并且需要成为域管理员。

    > [!IMPORTANT]
    > 无论在委派选项卡上为 C2WTS 服务帐户配置何种设置，都需要与正在使用的主服务帐户匹配。 对于报表查看器 Web 部件，这是 SharePoint Web 应用程序的服务帐户。 对于 SharePoint 集成模式，这是 Reporting Services 服务帐户。
    >
    > 例如，如果允许将 C2WTS 服务帐户委派给 SQL 服务，则需要对 SharePoint 集成模式的 Reporting Services 服务帐户执行相同操作。

    * 右键单击各服务帐户并且打开“属性”对话框。 在该对话框中，单击 **“委派”** 选项卡。

        只有在对象具有分配给它的服务主体名 (SPN) 的情况下，“委派”选项卡才可见。 C2WTS 不要求在 C2WTS 帐户上具有 SPN；但如果没有 SPN，“委派”选项卡将不可见。 配置约束委派的另一个方法是使用 **ADSIEdit**之类的实用工具。

    * “委派”选项卡上的主要配置选项如下：

        * 选择“仅信任此用户对指定服务的委派”
        * 选择“使用任何身份验证协议”

    * 选择“添加”以添加要委派的服务。

    * 选择“用户或计算机...”并输入托管服务的帐户*。 例如，如果在名为 sqlservice 的帐户下运行 SQL Server，则输入 `sqlservice`。 

    * 选择服务列表。 将显示该帐户可用的 SPN。 如果在该帐户上没有看到列出的服务，则它可能已丢失或放置在不同的帐户上。 可以使用 SetSPN 实用工具调整 SPN。

    * 选择“确定”以退出对话框。

3. 配置 C2WTS“AllowedCallers”。

    C2WTS 需要在配置文件 C2WTShost.exe.config 中显式列出的“调用方”标识。C2WTS 不接受来自系统中所有验证了身份的用户的请求，除非配置为这样做。 在此情况下，“调用方”是 WSS_WPG Windows 组。 C2WTShost.exe.confi 文件保存在以下位置：

    在 SharePoint 管理中心为 C2WTS 服务更改服务帐户，会将该帐户添加到 WSS_WPG 组中。

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

4. 在“管理服务器上的服务”页，通过 SharePoint 管理中心启动 Claims to Windows Token Service。 应在将执行操作的服务器上启动该服务。 例如，如果你有一个作为 WFE 的服务器，并且有另一个作为应用程序服务器的服务器（该服务器正在运行 SQL Server Reporting Services 共享服务），则只需在该应用程序服务器上启动 C2WTS。 如果在运行报表查看器 Web 部件，则仅 WFE 服务器上需要 C2WTS。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
