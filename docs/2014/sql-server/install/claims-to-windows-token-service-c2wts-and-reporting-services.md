---
title: 声明为 Windows 令牌服务（C2WTS）和 Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0ec82b7cca2062e1ed918e300eeb76dad16cbb20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245621"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) 和 Reporting Services
  如果要对 SharePoint 场之外的数据源使用 windows 身份验证[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，则需要使用 sharepoint 模式下的 sharepoint 声明到 Windows 令牌服务（c2WTS）。 即使用户使用 Windows 身份验证访问数据源，上述要求也是成立的。其原因在于，Web 前端 (WFE) 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务之间的通信将始终是 Claims 身份验证。  
  
 即使你的数据源与共享服务位于相同的计算机上，也需要 c2WTS。 但在此方案中，不需要约束委派。  
  
 c2WTS 创建的令牌将仅用于约束委派（对特定服务的约束）以及配置选项“使用任何身份验证协议”。 如前所述，如果您的数据源与共享服务位于同一台计算机上，则不需要约束委派。  
  
 如果您的环境将使用 Kerberos 约束委派，则 SharePoint 服务器服务和外部数据源需要位于同一 Windows 域中。 依赖于 Claims to Windows Token Service (c2WTS) 的所有服务都必须使用 Kerberos **约束** 委派，以便允许 c2WTS 使用 Kerberos 协议转换将声明转换为 Windows 凭据。 这些规定适用于所有 SharePoint 共享服务。 有关详细信息，请参阅[Microsoft SharePoint 2010 产品的 Kerberos 身份验证概述https://technet.microsoft.com/library/gg502594.aspx)（](https://technet.microsoft.com/library/gg502594.aspx)。  
  
 本主题将概述此过程。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
## <a name="prerequisites"></a>必备条件  
  
> [!NOTE]  
>  请注意，某些配置步骤可能会更改，或者在某些场拓扑中不适用。 例如，单服务器安装并不支持 Windows Identity Foundation c2WTS 服务，因此，在该场配置中不可能实现 Claims to Windows Token 委派方案。  
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>配置 c2WTS 所需的基本步骤  
  
1.  配置 c2WTS 服务帐户。 将该服务帐户添加到运行 c2WTS 的每个应用程序服务器上的本地管理员组。 此外，确认该帐户具有以下本地安全策略权限：  
  
    -   以操作系统方式操作  
  
    -   在身份验证后模拟客户端  
  
    -   作为服务登录  
  
     你用于 c2WTS 的帐户还需要配置为具有协议转换的约束委派，并且需要权限以便委派给需要与之通信的服务（即，SQL Server 引擎，SQL Server Analysis Services）。若要配置委派，可以使用 "Active Directory 用户和计算机" 管理单元。  
  
    1.  右键单击各服务帐户并且打开“属性”对话框。 在该对话框中，单击 **“委派”** 选项卡。  
  
        > [!NOTE]  
        >  请注意，只有在对象具有分配给它的 SPN 的情况下，“委派”选项卡才可见。 c2WTS 不要求在 c2WTS 帐户上使用 SPN，但如果没有 SPN，"**委派**" 选项卡将不可见。 配置约束委派的另一个方法是使用 **ADSIEdit**之类的实用工具。  
  
    2.  “委派”选项卡上的主要配置选项如下：  
  
        -   选择 "仅信任此用户来委派指定的服务"  
  
        -   选择 "使用任何身份验证协议"  
  
         有关详细信息，请参阅以下白皮书中的 "为计算机和服务帐户配置 Kerberos 约束委派" 部分，[配置适用于 SharePoint 2010 的 kerberos 身份验证和 SQL Server 2008 R2 产品](https://blogs.technet.com/b/tothesharepoint/archive/2010/07/22/whitepaper-configuring-kerberos-authentication-for-sharepoint-2010-and-sql-server-2008-r2-products.aspx)  
  
2.  配置 c2WTS "AllowedCallers"  
  
     c2WTS 要求在配置文件**c2wtshost.exe.config**中显式列出的 "调用方" 标识。c2WTS 不接受系统中所有经过身份验证的用户的请求，除非已将其配置为执行此操作。 在此情况下，“调用方”是 WSS_WPG Windows 组。 该 c2wtshost.exe.confi 文件保存在以下位置：  
  
     **\Program Files\Windows 标识 Foundation\v3.5\c2wtshost.exe.config**  
  
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
  
3.  启动操作系统 c2WTS 服务：  
  
    1.  配置该服务以便使用您在之前的步骤中配置的服务帐户。  
  
    2.  将启动类型更改为 "**自动**"，并启动服务。  
  
4.  在 "**管理服务器上的服务**" 页上，启动 sharepoint 的 "声明到 Windows 令牌服务"：通过 SharePoint 管理中心启动对 Windows 令牌服务的声明。 应在将执行操作的服务器上启动该服务。 例如，如果你有一个作为 WFE 的服务器，并且有另一个作为应用程序服务器的服务器（该服务器具有正在运行的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共享服务），则只需启动该应用程序服务器上的 c2WTS。 在 WFE 上不需要 c2WTS。  
  
## <a name="see-also"></a>另请参阅  
 [声明为 Windows 令牌服务（c2WTS）概述（https://msdn.microsoft.com/library/ee517278.aspx)](https://msdn.microsoft.com/library/ee517278.aspx)   
 [Microsoft SharePoint 2010 产品的 Kerberos 身份验证概述（https://technet.microsoft.com/library/gg502594.aspx)](https://technet.microsoft.com/library/gg502594.aspx)  
  
