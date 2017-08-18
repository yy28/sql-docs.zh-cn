---
title: "使用扩展保护连接到数据库引擎 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 894f04fe8bf8df95bb288acab897f3274fbacb18
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>使用扩展保护连接到数据库引擎
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自  始支持扩展保护 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。 **针对验证的扩展保护** 是操作系统实现的一项网络组件功能。 Windows 7 和 Windows Server 2008 R2 支持**扩展保护** 。 旧**操作系统的 Service Pack 中包括** 扩展保护 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 功能。 使用**扩展保护**进行连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会更安全。  
  
> [!IMPORTANT]  
>  默认情况下，Windows 不启用 **扩展保护** 。 有关如何在 Windows 中启用 **扩展保护** 的信息，请参阅 [针对验证的扩展保护](http://support.microsoft.com/kb/968389)。  
  
## <a name="description-of-extended-protection"></a>扩展保护的描述  
 **扩展保护** 使用服务绑定和渠道绑定来帮助防止身份验证中继攻击。 在身份验证中继攻击中，可以执行 NTLM 身份验证的客户端（例如，Windows Explorer、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook、.NET SqlClient 应用程序等）连接到攻击者（例如，恶意的 CIFS 文件服务器）。 攻击者使用客户端的凭据来伪装成此客户端并经受服务（例如， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务的实例）对其进行身份验证。  
  
 这种攻击具有两种变体：  
  
-   在引诱攻击中，客户端被引诱而自主连接到攻击者。  
  
-   在假冒攻击中，客户端打算连接到有效的服务，但没觉察到 DNS 和 IP 路由之一或两者已受到感染而将连接重定向到攻击者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持服务绑定和渠道绑定，以帮助减少在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上出现这些攻击。  
  
### <a name="service-binding"></a>服务绑定  
 服务绑定解决引诱攻击，它是通过要求客户端发送该客户端要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的一个签名服务主体名称 (SPN) 来实现的。 作为身份验证响应的一部分，此服务验证在数据包中收到的 SPN 与其自己的 SPN 匹配。 如果客户端被引诱连接到攻击者，则客户端将包含攻击者的已签名 SPN。 攻击者无法作为客户端来中继数据包以对实际 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务进行身份验证，因为它包含攻击者的 SPN。 服务绑定引发的成本是一次性的且微不足道，但它无法解决假冒攻击。 客户端应用程序不使用加密方式连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，发生服务绑定。  
  
### <a name="channel-binding"></a>渠道绑定  
 通道绑定在客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的实例之间建立安全通道 (Schannel)。 此服务通过将客户端特定于该通道的通道绑定标记 (CBT) 与其自己的 CBT 进行比较，验证客户端的身份。 渠道绑定可同时解决引诱攻击和假冒攻击。 然而，它引发的运行时成本较高，因为它要求对所有会话流量进行传输层安全 (TLS) 加密。 客户端应用程序使用加密方式连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，发生通道绑定，这与加密由客户端还是服务器实施无关。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 数据提供程序支持 TLS 1.0 和 SSL 3.0。 如果通过在操作系统 SChannel 层中进行更改来强制使用不同的协议（例如 TLS 1.1 或 TLS 1.2），你可能无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="operating-system-support"></a>操作系统支持  
 以下链接提供有关 Windows 如何支持 **扩展保护**的详细信息：  
  
-   [具有扩展保护的集成 Windows 身份验证](http://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Microsoft 安全建议 (973811)，针对验证的扩展保护](http://www.microsoft.com/technet/security/advisory/973811.mspx)  
  
## <a name="settings"></a>设置  
 三种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接设置可影响服务绑定和渠道绑定。 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器或使用 WMI 来配置这些设置，并可以使用基于策略的管理的 **服务器协议设置** 方面来查看这些设置。  
  
-   **强行加密**  
  
     可能的值为 **“打开”** 和 **“关闭”**。 若要使用渠道绑定，“强行加密”  必须设置为“打开” ，所有客户端都将强制进行加密。 如果为 **“关闭”**，则只确保服务绑定。 “强行加密” 位于 **配置管理器中的“MSSQLSERVER 的协议属性”（“标志”选项卡）**  [!INCLUDE[ssNoVersion](../../cludes/ssnoversion-md.md)] 上。  
  
-   **扩展保护**  
  
     可能的值为 **“关闭”**、 **“允许”**和 **“必需”**。 通过 **扩展保护** 变量，用户可以为每个  实例配置扩展保护 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 级别。 “扩展保护” 位于 **配置管理器中的“MSSQLSERVER 的协议属性”（“高级”选项卡）**  [!INCLUDE[ssNoVersion](../../cludes/ssnoversion-md.md)] 上。  
  
    -   当设置为 **“关闭”**时，禁用 **扩展保护** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例将接受来自任何客户端的连接，不管该客户端是否受保护。 **“关闭”** 选项虽与旧的和未打补丁的操作系统兼容，但安全性较差。 当您知道客户端操作系统不支持扩展保护时，请使用此设置。  
  
    -   当设置为 **“允许”**时，来自支持 **扩展保护** 的操作系统的连接需要 **扩展保护**。 来自不支持**扩展保护** 的操作系统的连接将忽略 **扩展保护**。 来自运行在受保护客户端操作系统上的不受保护客户端应用程序的连接被拒绝。 此设置虽比 **“关闭”**更安全，但仍不是最安全的设置。 在混合环境（即有些操作系统支持 **扩展保护** ，有些不支持）中使用此设置。  
  
    -   当设置为 **“必需”**时，只接受来自受保护操作系统上受保护应用程序的连接。 此设置是最安全的，但来自不支持 **扩展保护** 的操作系统或应用程序的连接将无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   **接受的 NTLM SPN**  
  
     当多个 SPN 知道一个服务器时，需要 **“接受的 NTLM SPN”** 变量。 当客户端尝试使用服务器不知道的有效 SPN 连接到服务器时，服务绑定将失败。 为避免此问题，用户可以使用 **“接受的 NTLM SPN”**指定表示服务器的多个 SPN。 **“接受的 NTLM SPN”** 是一系列由分号分隔的 SPN。 例如，若要允许 SPN **MSSQLSvc/ HostName1.Contoso.com** 和 **MSSQLSvc/ HostName2.Contoso.com**，请在“接受的 NTLM SPN”  框中键入 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** 。 变量的最大长度为 2048 个字符。 “接受的 NTLM SPN” 位于 **配置管理器中的“MSSQLSERVER 的协议属性”（“高级”选项卡）**  [!INCLUDE[ssNoVersion](../../cludes/ssnoversion-md.md)] 上。  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>为数据库引擎启用扩展保护  
 若要使用 **扩展保护**，服务器和客户端都必须具有支持 **扩展保护**的操作系统，并且必须在操作系统上启用 **扩展保护** 。 有关如何为操作系统启用 **扩展保护** 的详细信息，请参阅 [针对验证的扩展保护](http://support.microsoft.com/kb/968389)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自  始支持扩展保护 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。  的某些早期版本的扩展保护 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在后续的更新中提供。 在服务器计算机上启用 **扩展保护** 之后，使用以下步骤启用 **扩展保护**：  
  
1.  在 **“开始”** 菜单上，选择 **“所有程序”**，指向 **Microsoft SQL Server** ，再单击 **“SQL Server 配置管理器”**。  
  
2.  展开“SQL Server 网络配置” 、右键单击“  *\<**>*，然后单击“属性” 。  
  
3.  对于渠道绑定和服务绑定，同时在 **“高级”** 选项卡上将 **“扩展保护”** 设置为适当的设置。  
  
4.  或者，当多个 SPN 知道一个服务器时，在 **“高级”** 选项卡上按照“设置”部分所述配置 **“接受的 NTLM SPN”** 字段。  
  
5.  对于渠道绑定，在 **“标志”** 选项卡上，将 **“强行加密”** 设置为 **“打开”**。  
  
6.  重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务。  
  
## <a name="configuring-other-sql-server-components"></a>配置其他 SQL Server 组件  
 有关如何配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的详细信息，请参阅 [Reporting Services 针对身份验证的扩展保护](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)。  
  
 当通过 HTTP 连接或 HTTPS 连接使用 IIS 访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以利用 IIS 提供的扩展保护。 有关配置 IIS 使用扩展保护的详细信息，请参阅 [Configure Extended Protection in IIS 7.5（在 IIS 7.5 中配置扩展保护）](http://go.microsoft.com/fwlink/?LinkId=181105)。  
  
## <a name="see-also"></a>另请参阅  
 [服务器网络配置](../../database-engine/configure-windows/server-network-configuration.md)   
 [客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)   
 [针对验证的扩展保护概述](http://go.microsoft.com/fwlink/?LinkID=177943)   
 [具有扩展保护的集成 Windows 身份验证](http://go.microsoft.com/fwlink/?LinkId=179922)  
  
  
