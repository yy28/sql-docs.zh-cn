---
title: "Claims to Windows Token Service (c2WTS) 和 Reporting Services |Microsoft 文档"
ms.custom: The Claims to Windows Token Service (C2WTS) is used by SharePoint and needs to be configured for Kerberos constrained delegation to work with SQL Server Reporting Services properly.
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 8a478bba3cde66967594d5ef02f867de5b33edd7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/15/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) 和 Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

如果你想要查看在本机模式报表，则需要 SharePoint Claims to Windows Token Service (C2WTS) [SQL Server Reporting Services 报表查看器 web 部件](../report-server-sharepoint/deploy-report-viewer-web-part.md)。

如果你想要对 SharePoint 场之外的数据源使用 Windows 身份验证，则也与 SQL Server Reporting Services SharePoint 模式需要 C2WTS。 即使您的数据源与共享服务位于相同的计算机上，也需要 C2WTS。 但在此方案中，不需要约束委派。

> [!NOTE]
> 与 SharePoint 的 reporting Services 集成 SQL Server 2016 之后将不再可用。

## <a name="report-viewer-web-part-configuration"></a>报表查看器 web 部件配置

可以使用报表查看器 web 部件嵌入 SharePoint 站点中的 SQL Server Reporting Services 本机模式报表。 此 web 部件是可用于 SharePoint 2013 和 SharePoint 2016。 SharePoint 2013 和 SharePoint 2016 使得使用的声明的身份验证。 默认情况下，SQL Server Reporting Services （本机模式） 使用 Windows 身份验证。 因此，C2WTS 需要正确配置以便正确呈现的报表。

## <a name="sharepoint-mode-integaration"></a>SharePoint 模式 integaration

**本部分仅适用到 SQL Server 2016 Reporting Services 及更早版本。**

如果你想要对 SharePoint 场之外的数据源使用 Windows 身份验证 SharePoint Claims to Windows Token Service (C2WTS) 需要与 SQL Server Reporting Services SharePoint 模式。 即使用户访问使用 Windows 身份验证的数据源，因为之间的通信 web 前端 (WFE) 和 Reporting Services 共享的服务将始终为声明的身份验证，也是如此。

## <a name="steps-needed-to-configure-c2wts"></a>配置 c2WTS 所需的步骤

C2WTS 创建的令牌将仅用于约束委派（对特定服务的约束）以及配置选项“使用任何身份验证协议”。 如前所述，如果您的数据源与共享服务位于同一台计算机上，则不需要约束委派。

如果您的环境将使用 Kerberos 约束委派，则 SharePoint 服务器服务和外部数据源需要位于同一 Windows 域中。 依赖于 Claims to Windows Token Service (c2WTS) 的所有服务都必须使用 Kerberos **约束** 委派，以便允许 c2WTS 使用 Kerberos 协议转换将声明转换为 Windows 凭据。 这些规定适用于所有 SharePoint 共享服务。 有关详细信息，请参阅 [在 SharePoint 2013 中规划 Kerberos 身份验证](http://technet.microsoft.com/library/ee806870.aspx)。  

1. 配置 C2WTS 服务帐户。 将服务帐户添加到 C2WTS，将会使用每个服务器上的本地管理员组。

    有关**报表查看器 web 部件**，这将是 Web 前端 (WFE) 服务器。 有关**SharePoint 集成模式下**，这将是 Reporting Services 服务正在其中运行的应用程序服务器。

2. 配置 C2WTS 服务帐户的委派。

    该帐户需要具有协议转换和权限以便委派给它的所需进行通信 （即 SQL Server 数据库引擎，SQL Server Analysis Services） 的服务的约束委派。 若要配置委派你可以使用 Active Directory 用户和计算机管理单元中，并且将需要是域管理员。

    > [!IMPORTANT]
    > 任何设置你配置 C2WTS 服务帐户，在委派选项卡上，需要匹配主服务所使用的帐户。 有关**报表查看器 web 部件**，这将是 SharePoint web 应用程序的服务帐户。 有关**SharePoint 集成模式下**，这将是 Reporting Services 服务帐户。
    >
    > 例如，如果你允许 C2WTS 服务帐户委派给 SQL 服务，你需要执行相同的在 SharePoint 集成模式下的 Reporting Services 服务帐户。

    * 右键单击各服务帐户并且打开“属性”对话框。 在该对话框中，单击 **“委派”** 选项卡。

        委派选项卡才可见，如果该对象具有服务主体名称 (SPN) 分配给它。 C2WTS 不要求在 C2WTS 帐户上的 SPN 但是，如果没有 SPN，**委派**选项卡将不可见。 配置约束委派的另一个方法是使用 **ADSIEdit**之类的实用工具。

    * “委派”选项卡上的主要配置选项如下：

        * 选择**信任仅委派到指定服务的用户**
        * 选择**使用任何身份验证协议**

    * 选择“添加”以添加要委派的服务。

    * 选择**用户或计算机...*** 并输入承载服务的帐户。 例如，如果名为的帐户下运行 SQL Server *sqlservice*，输入`sqlservice`。 

    * 选择服务列表。 将显示该帐户可用的 SPN。 如果在该帐户上没有看到列出的服务，则它可能已丢失或放置在不同的帐户上。 可以使用 SetSPN 实用工具调整 SPN。

    * 选择“确定”以退出对话框。

3. 配置 C2WTS *AllowedCallers*。

    C2WTS 需要调用方标识显式配置文件中列出**C2WTShost.exe.config**。C2WTS 不接受来自系统中所有验证了身份的用户的请求，除非配置为这样做。 在这种情况下，调用方是 WSS_WPG Windows 组。 C2WTShost.exe.confi 文件保存在以下位置：

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

4. 在上启动 Claims to Windows Token Service 通过 SharePoint 管理中心**管理服务器上的服务**页。 应在将执行操作的服务器上启动该服务。 例如，如果你有一台服务器，它是 WFE 服务器和另一台服务器是具有 SQL Server Reporting Services 共享的服务正在运行、 仅对你的应用程序服务器需要启动的应用程序服务器上的 C2WTS。 如果你正在运行的报表查看器 web 部件，C2WTS 仅需要在 WFE 服务器上。

更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
