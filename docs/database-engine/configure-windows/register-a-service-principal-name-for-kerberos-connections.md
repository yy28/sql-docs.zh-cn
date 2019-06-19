---
title: 为 Kerberos 连接注册服务主体名称 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: b36c25969ac053bad4e626b110c314c28dff6b08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66772155"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>为 Kerberos 连接注册服务主体名称
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要将 Kerberos 身份验证用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则以下两个条件都必须得到满足：  
  
-   客户端计算机和服务器计算机必须属于同一 Windows 域或在可信域中。  
  
-   服务主体名称 (SPN) 必须在 Active Directory 中进行注册，后者在 Windows 域中起到密钥分发中心的作用。 SPN 在注册后会映射到启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例服务的 Windows 帐户。 如果未进行 SPN 注册或注册失败，则 Windows 安全层无法确定与 SPN 关联的帐户，因而无法使用 Kerberos 身份验证。  
  
    > [!NOTE]  
    >  如果服务器无法自动注册 SPN，则必须手动注册 SPN。 请参阅 [手动注册 SPN](#Manual)。  
  
可以通过查询 sys.dm_exec_connections 动态管理视图来验证连接使用的是否为 Kerberos。 请运行下面的查询并检查 auth_scheme 列的值，如果 Kerberos 已启用，该值应为“KERBEROS”。  
  
```sql  
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;  
```  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一款诊断工具，可帮助解决与 Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相关的连接问题。 有关详细信息，请参阅 [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046)。  
  
##  <a name="Role"></a> SPN 在身份验证过程中所起的作用  
 当应用程序打开一个连接并使用 Windows 身份验证时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 会传递 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机名、实例名和 SPN（可选）。 如果该连接传递了 SPN，则使用它时不对它做任何更改。  
  
 如果该连接未传递 SPN，则将根据所使用的协议、服务器名和实例名构造一个默认的 SPN。  
  
 在上面这两种情况下，都会将 SPN 发送到密钥分发中心以获取用于对连接进行身份验证的安全标记。 如果无法获取安全标记，则身份验证采用 NTLM。  
  
 服务主体名称 (SPN) 是客户端用来唯一标识服务实例的名称。 Kerberos 身份验证服务可以使用 SPN 对服务进行身份验证。 当客户端想要连接到某个服务时，它将查找该服务的实例，并为该实例编写 SPN，然后连接到该服务并显示该服务的 SPN 以进行身份验证。  
  
> [!NOTE]  
>  本主题中提供的信息还适用于使用聚类分析的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置。  
  
 Windows 身份验证是向 SQL Server 验证用户身份的首选方法。 使用 Windows 身份验证的客户端通过 NTLM 或 Kerberos 进行身份验证。 在 Active Directory 环境中，始终首先尝试 Kerberos 身份验证。 Kerberos 身份验证不可用于使用命名管道的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 客户端。  
  
##  <a name="Permissions"></a> 权限  
 当启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务时，它将尝试注册服务主体名称 (SPN)。 如果启动 SQL Server 的帐户没有在 Active Directory 域服务中注册 SPN 的权限，则此调用将失败，并将在应用程序事件日志以及 SQL Server 错误日志中记录一条警告消息。 若要注册 SPN，必须在内置帐户（如 Local System（建议不要使用）或 NETWORK SERVICE）或有权注册 SPN 的帐户（如域管理员帐户）下运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或  [!INCLUDE[win7](../../includes/win7-md.md)] 操作系统上运行  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 时，可以使用虚拟帐户或托管服务帐户 (MSA) 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 虚拟帐户和 MSA 都可以注册 SPN。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不在上述任一帐户下运行，则启动时不会注册 SPN，此时，域管理员必须手动注册 SPN。  
  
> [!NOTE]  
>  将 Windows 域配置为在低于 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Windows Server 2008 R2 功能级别的级别上运行时，托管服务帐户将不具有注册 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服务的 SPN 所需的权限。 如果需要进行 Kerberos 身份验证，域管理员应手动在托管服务帐户上注册 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SPN。  
  
 知识库文章 [How to use Kerberos authentication in SQL Server](https://support.microsoft.com/kb/319723)（如何在 SQL Server 中使用 Kerberos 身份验证）包含有关如何向非域管理员帐户授予 SPN 读或写权限的信息。  
  
 有关其他信息，请参阅 [How to Implement Kerberos Constrained Delegation with SQL Server 2008](https://technet.microsoft.com/library/ee191523.aspx)（如何使用 SQL Server 2008 实现 Kerberos 约束委派）  
  
##  <a name="Formats"></a> SPN 格式  
 自 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]开始，SPN 格式已发生更改，目的是为了支持对 TCP/IP、Named Pipes 和 Shared Memory 进行 Kerberos 身份验证。 所支持的命名实例和默认实例的 SPN 格式如下所示。  
  
**命名实例**  
  
-   MSSQLSvc/\<FQDN>:[\<port> | \<instancename>]其中  ：  
  
    -   **MSSQLSvc** 是要注册的服务。  
  
    -   **\<FQDN>** 是服务器的完全限定域名。  
  
    -   **\<port>** 是 TCP 端口号。  
  
    -   **\<instancename>** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。  
  
**默认实例**  
  
-   MSSQLSvc/\<FQDN>:\<port> | MSSQLSvc/\<FQDN>，其中   ：  
  
    -   **MSSQLSvc** 是要注册的服务。  
  
    -   **\<FQDN>** 是服务器的完全限定域名。  
  
    -   **\<port>** 是 TCP 端口号。  
  
    > [!NOTE]
    > 新 SPN 格式不需要端口号。 这意味着，多端口服务器或不使用端口号的协议都可以使用 Kerberos 身份验证。  
   
|||  
|-|-|  
|MSSQLSvc/\<FQDN>:<port>|使用 TCP 时访问接口生成的默认 SPN。 \<port> 是 TCP 端口号。|  
|MSSQLSvc/\<FQDN>|使用除 TCP 之外的协议时访问接口生成的用于默认实例的默认 SPN。 \<FQDN> 为完全限定的域名。|  
|MSSQLSvc/\<FQDN>:\<instancename>|使用除 TCP 之外的协议时访问接口生成的用于命名实例的默认 SPN。 \<instancename> 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例名称。|  

> [!NOTE]  
> 对于 TCP/IP 连接，由于 SPN 中包括 TCP 端口，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须启用 TCP 协议，以便用户使用 Kerberos 身份验证进行连接。 

##  <a name="Auto"></a> 自动注册 SPN  
 当 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例启动时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将尝试为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务注册 SPN。 实例停止时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将尝试取消此 SPN 的注册。 对于 TCP/IP 连接，注册 SPN 时使用的格式为 MSSQLSvc/\<FQDN>:\<tcpport>   。命名实例和默认实例均将注册为 MSSQLSvc，可根据 \<tcpport> 值来区分这些实例   。  
  
 对于支持 Kerberos 的其他连接，为命名实例注册 SPN 时使用的格式为 MSSQLSvc/\<FQDN>/\<实例名>   。 注册默认实例的格式为 MSSQLSvc/\<FQDN>  。  
  
 如果服务帐户缺少执行这些操作所需的权限，在注册或取消注册 SPN 时可能需要进行手动干预。  
  
##  <a name="Manual"></a> 手动注册 SPN  
若要手动注册 SPN，管理员必须使用随 Microsoft [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 支持工具提供的 Setspn.exe 工具。 有关详细信息，请参阅 [Windows Server 2003 Service Pack 1 Support Tools](https://support.microsoft.com/kb/892777) （Windows Server 2003 Service Pack 1 支持工具）知识库文章。  
  
Setspn.exe 是一个命令行工具，您可通过该工具读取、修改和删除服务主体名称 (SPN) 目录属性。 您还可借助此工具查看当前 SPN、重置帐户的默认 SPN 以及添加或删除补充 SPN。  
  
以下示例说明了用于为使用域用户帐户的 TCP/IP 连接手动注册 SPN 的语法：  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```  
  
> [!NOTE]
> 如果 SPN 已存在，则必须在重新注册该 SPN 之前将其删除。 可以使用带有 `setspn` 开关的 `-D` 命令实现此操作。 以下示例说明如何手动注册基于新实例的 SPN。 对于使用域用户帐户的默认实例，使用：  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
对于命名实例，请使用：  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com/instancename redmond\accountname  
```  
  
##  <a name="Client"></a> 客户端连接  
 客户端驱动程序支持用户指定的 SPN。 但是，如果未提供 SPN，则将根据客户端连接类型自动生成 SPN。 对于 TCP 连接，为命名实例和默认实例使用 *MSSQLSvc*/*FQDN*:[*port*] 格式的 SPN。  
  
对于 Named Pipes 和 Shared Memory 连接，对命名实例使用 MSSQLSvc/\<FQDN>:\<instancename> 格式的 SPN，对默认实例使用 MSSQLSvc/\<FQDN> 格式   。  
  
 **将服务帐户用作 SPN**  
  
可将服务帐户用作 SPN。 可以通过 Kerberos 身份验证的连接属性指定服务帐户，并采用以下格式：  
  
-   **username@domain** 操作系统上运行 **domain\username** （适用于域用户帐户）  
  
-   machine$@domain 或 host\FQDN（适用于计算机域帐户，如 Local System 或 NETWORK SERVICES）   。  
  
若要确定连接的身份验证方法，请执行下面的查询。  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
##  <a name="Defaults"></a> 身份验证默认值  
 下表说明根据 SPN 注册情况所使用的身份验证默认值。  
  
|应用场景|身份验证方法|  
|--------------|---------------------------|  
|SPN 映射到正确的域帐户、虚拟帐户、MSA 或内置帐户。 例如 Local System 或 NETWORK SERVICE。|本地连接使用 NTLM，远程连接使用 Kerberos。|  
|SPN 是正确的域帐户、虚拟帐户、MSA 或内置帐户。|本地连接使用 NTLM，远程连接使用 Kerberos。|  
|SPN 映射到不正确的域帐户、虚拟帐户、MSA 或内置帐户。|身份验证失败。|  
|SPN 查找失败或未映射到正确的域帐户、虚拟帐户、MSA 或内置帐户，或者不是正确的域帐户、虚拟帐户、MSA 或内置帐户。|本地和远程连接使用 NTLM。|  
  
> [!NOTE]  
> “正确”表示注册的 SPN 映射到的帐户是当前运行 SQL Server 服务的帐户。  
  
##  <a name="Comments"></a> 注释  
 专用管理员连接 (DAC) 使用一个基于实例名称的 SPN。 如果成功注册 SPN，则可以将 Kerberos 身份验证用于 DAC。 用户也可以选择将帐户名指定为 SPN。  
  
 如果在启动过程中 SPN 注册失败，将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中记录此失败，而启动过程将继续进行。  
  
 如果在关闭时 SPN 取消注册失败，将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中记录此失败，而关闭过程将继续进行。  
  
## <a name="see-also"></a>另请参阅  
 [客户端连接中的服务主体名称 (SPN) 支持](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)   
 [客户端连接中的服务主体名称 (SPN) (OLE DB)](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)   
 [客户端连接中的服务主体名称 (SPN) (ODBC)](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)   
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [管理 Reporting Services 环境中的 Kerberos 身份验证问题](https://technet.microsoft.com/library/ff679930.aspx)  
  
  
