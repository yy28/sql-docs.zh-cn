---
title: 排查连接到 SQL Server 数据库引擎时的问题 | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 321ae7aea8a8d3742f641e57d5a8c4276938a555
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665227"
---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>排查连接到 SQL Server 数据库引擎时发生的问题
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

这是在无法连接到 SQL Server 数据库引擎时使用的故障排除技术的详尽列表。 这些步骤不按你可能已尝试过的最有可能出现的问题顺序排序， 而按从最基本问题到更复杂问题的顺序排序。 这些步骤假定你使用 TCP/IP 协议从另一台计算机连接到 SQL Server（这是最常见的情形）。 这些步骤针对 SQL Server 和客户端应用程序均运行 Windows 10 的 SQL Server 2016 而编写，不过，这些步骤通常也适用于其他版本的 SQL Server 和其他操作系统，只需进行细微的修改即可。

在排查“连接到服务器”错误（可能为错误编号：11001（或 53），严重性：20，状态：0）和如下错误消息时，这些说明特别有用：

*   “在与 SQL Server 建立连接时出现与网络相关的或特定于实例的错误。 找不到服务器或服务器无法访问。 请验证实例名称是正确的，且将 SQL Server 配置为允许远程连接。 " 

*   “(提供程序: 命名管道提供程序，错误: 40 - 无法打开到 SQL Server 的连接) (Microsoft SQL Server，错误: 53)”或“(提供程序: TCP 提供程序，错误: 0 - 此主机不存在。) (Microsoft SQL Server，错误: 11001)” 

此错误通常意味着找不到 SQL Server 计算机，或者 TCP 端口号要么未知，要么不是正确的端口号，要么被防火墙阻止。

>  [!TIP]
>  有关交互式故障排除页面，请参阅 [!INCLUDE[msCoName_md](../../includes/msconame-md.md)] 客户支持服务中的 [Solving Connectivity errors to SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)（解决到 SQL Server 的连接问题）。

### <a name="not-included"></a>不包含的信息

* 本主题不包含有关 SSPI 错误的信息。 有关 SSPI 错误，请参阅 [如何排查“无法生成 SSPI 上下文”错误消息](http://support.microsoft.com/kb/811889)。  
* 本主题不包含有关 Kerberos 错误的信息。 有关帮助，请参阅 [Microsoft Kerberos Configuration Manager for SQL Server](http://www.microsoft.com/download/details.aspx?id=39046)。
* 本主题不包含有关 SQL Azure 连接的信息。 有关帮助，请参阅[排查 Microsoft Azure SQL 数据库的连接问题](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database)。 

## <a name="gathering-information-about-the-instance-of-sql-server"></a>收集 SQL Server 实例的相关信息

首先，必须收集有关数据库引擎的基本信息。

1. 确认 SQL Server 数据库引擎实例已安装并且正在运行。
    1.  登录到托管 SQL Server 实例的计算机。
    2.  启动 SQL Server 配置管理器。 （安装 SQL Server 时，会自动在计算机上安装配置管理器。 SQL Server 和 Windows 版本的配置管理器启动说明略有不同。 有关启动配置管理器的帮助，请参阅 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。
    3.  在配置管理器的左窗格中，选择“SQL Server 服务”。 在右窗格中，确认数据库引擎实例已存在并且正在运行。 名为 **SQL Server (MSSQLSERVER)** 的实例是默认（未命名）实例。 只能有一个默认实例。 其他（已命名）实例将用括号括住其名称。 SQL Server Express 使用名称 **SQL Server (SQLEXPRESS)** 作为实例名称，除非有人在安装过程中将其命名为其他名称。 请记下你尝试连接到的实例的名称。 另外，通过查找绿色箭头确认该实例正在运行。 如果该实例显示红色方块，则右键单击该实例，然后单击“启动”。 它应变为绿色。
     4. 如果你正在尝试连接到命名实例，请确保 SQL Server Browser 服务正在运行。
 

2.  获取计算机的 IP 地址。
    1. 在“开始”菜单上，单击“运行”。 在“运行”窗口中键入 **cmd**，然后单击“确定”。
    2.  在命令提示符窗口中键入 **ipconfig** ，然后按 Enter。 记下 **IPv4** 地址和 **IPv6** 地址。 （SQL Server 可以使用较旧的 IP 版本 4 协议或较新的 IP 版本 6 协议进行连接。 你的网络可能允许其中某种协议，或者两种协议都允许。 多数用户首先会排查 **IPv4** 地址问题。 它更短且更容易键入。）


3.  获取 SQL Server 所用的 TCP 端口号。 在大多数情况下，你会使用 TCP 协议从另一台计算机连接到数据库引擎。
    1.  在运行 SQL Server 的计算机上使用 SQL Server Management Studio 连接到 SQL Server 实例。 在对象资源管理器中，展开“管理”，展开“SQL Server 日志”，然后双击当前日志。
    2.  在日志查看器中，单击工具栏上的“筛选器”按钮。 在“消息包含文本”框中，键入**服务器正在侦听**，单击“应用筛选器”，然后单击“确定”。
    3.  应列出一条类似于“服务器正在侦听 [ 'any' \<ipv4> 1433]”的消息。 此消息表示，此 SQL Server 实例正在侦听此计算机上的所有 IP 地址（针对 IP 版本 4）和侦听 TCP 端口 1433。 （TCP 端口 1433 通常是由数据库引擎使用的端口。 一个端口只允许由一个 SQL Server 实例使用，因此，如果安装了多个 SQL Server 实例，某些实例必须使用其他端口号。）请记下由你尝试连接到的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例使用的端口号。 

    >    [!NOTE] 
    >    可能会列出 IP 地址 127.0.0.1。 它称为环回适配器地址，只能从同一台计算机上的进程连接到该地址。 它可用于故障排除，但你不能使用它从另一台计算机进行连接。

## <a name="enable-protocols"></a>启用协议

在某些 SQL Server 安装中，不支持从另一台计算机连接到数据库引擎，除非管理员使用配置管理器启用这种连接。 若要支持从另一台计算机进行连接，请执行以下操作：

1.  如前面所述，打开 SQL Server 配置管理器。 
2.  在配置管理器的左窗格中，展开“SQL Server 网络配置”，然后选择要连接到的 SQL Server 实例。 右窗格会列出可用的连接协议。 共享内存通常处于启用状态。 只能从同一台计算机使用共享内存，因此，大多数安装会将它保留为启用状态。 若要从另一台计算机连接到 SQL Server，通常将使用 TCP/IP。 如果未启用 TCP/IP，请右键单击“TCP/IP”，然后单击“启用”。 
3.  如果更改了任何协议的启用设置，则必须重新启动数据库引擎。 在左窗格中，选择“SQL Server 服务”。 在右窗格中，右键单击数据库引擎实例，然后单击“重新启动”。 

## <a name="testing-tcpip-connectivity"></a>测试 TCP/IP 连接

使用 TCP/IP 连接到 SQL Server 时，要求 Windows 可以建立连接。 使用 `ping` 工具测试 TCP。
1.  在“开始”菜单上，单击“运行”。 在“运行”窗口中键入 **cmd**，然后单击“确定”。 
2.  在命令提示符窗口中，键入 `ping`，然后键入正在运行 SQL Server 的计算机的 IP 地址。 例如，使用 IPv4 地址 `ping 192.168.1.101` ，或使用 IPv6 地址 `ping fe80::d51d:5ab5:6f09:8f48%11` 。 （必须将 ping 后面的数字替换为之前在计算机上收集的 IP 地址。） 
3.  如果网络配置正确，将收到一条响应，例如，“来自 \<IP 地址> 的回复”，后跟一些附加信息。 如果收到一个错误，例如“无法访问目标主机。” 或“请求超时。”，表示 TCP/IP 配置不正确。 （确保 IP 地址正确并且键入正确。）此时的错误可能表示客户端计算机、服务器计算机或某些网络相关设备（如路由器）出现了问题。 Internet 有许多可供排查 TCP/IP 问题的资源。 2006 年发布的 [如何排查基本 TCP/IP 问题](http://support.microsoft.com/kb/169790)一文是一个合理的起点。
4.  接下来，如果使用 IP 地址成功进行了 ping 测试，请测试计算机名称能否解析为 TCP/IP 地址。 在客户端计算机上的命令提示符窗口中，键入 `ping` ，然后键入正在运行 SQL Server 的计算机的计算机名称。 例如，使用 IPv4 地址 `ping newofficepc` 
5.  如果你本可以对 ipaddress 执行 ping 操作，而现在收到一个错误，如“无法访问目标主机。” 或“请求超时。”，表示客户端计算机上缓存的名称解析信息可能较旧（已过时）。 请键入 `ipconfig /flushdns` 以清除 DNS（动态名称解析）缓存。 然后再次使用名称 ping 计算机。 清除 DNS 缓存后，客户端计算机将检查服务器计算机的 IP 地址的最新相关信息。 
6.  如果网络配置正确，将收到一条响应，例如，“来自 \<IP 地址> 的回复”，后跟一些附加信息。 如果你可以使用 IP 地址成功 ping 服务器计算机，但在使用计算机名称执行 ping 操作时收到一个错误，例如，“无法访问目标主机。” 或“请求超时。”，表示名称解析配置不正确。 （有关详细信息，请参阅之前引用的 2006 年发布的[如何排查基本 TCP/IP 问题](http://support.microsoft.com/kb/169790)一文。）连接到 SQL Server 不需要成功的名称解析，但如果计算机名称无法解析为 IP 地址，则必须通过指定 IP 地址来建立连接。 这并不是理想的解决方法，但稍后可以修复名称解析。
  
  
## <a name="testing-a-local-connection"></a>测试本地连接

在从另一台计算机排查连接问题之前，首先测试你是否能够从运行 SQL Server 的计算机上安装的客户端应用程序进行连接。 （这将避免发生防火墙问题）。此过程使用 SQL Server Management Studio。 如果未安装 Management Studio，请参阅[下载 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。 （如果无法安装 Management Studio，则可以使用随数据库引擎一起安装的 `sqlcmd.exe` 实用工具来测试连接。 有关 `sqlcmd.exe`的信息，请参阅 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)。）
1.  使用有权访问 SQL Server 的登录名登录到安装了 SQL Server 的计算机。 （在安装期间，SQL Server 要求将至少一个登录名指定为 SQL Server 管理员。 如果不知道管理员，请参阅[在系统管理员被锁定时连接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md)。
2.   在“开始”页上键入 **SQL Server Management Studio**，或在旧版 Windows 的“开始”菜单上，指向“所有程序”，指向“Microsoft SQL Server”，然后单击“SQL Server Management Studio”。
3.  在“连接到服务器”对话框的“服务器类型”框中，选择“数据库引擎”。 在“身份验证”框中，选择“Windows 身份验证”。 在“服务器名称”框中，键入以下项之一：

|连接到：|类型：|例如：|
|-----------------|---------------|-----------------|
|默认实例|计算机名称|ACCNT27|
|命名实例|计算机名称\实例名称|ACCNT27\PAYROLL|

>  [!NOTE] 
>  当从同一台计算机上的客户端应用程序连接到 SQL Server 时，将使用共享内存协议。 共享内存是一种本地命名管道，因此有时会遇到管道方面的错误。

如果此时收到一个错误，则必须先解决它，然后才能继续操作。 有许多可能属于问题的情况。 你的登录名可能未获权进行连接。 你的默认数据库可能已丢失。

>    [!NOTE] 
>    某些传递到客户端的错误消息故意不提供足够的信息来排查问题。 这是一项安全功能，目的是避免为攻击者提供有关 SQL Server 的信息。 若要查看有关错误的完整信息，请查找 SQL Server 错误日志。 那里提供了详细信息。 如果收到错误 18456“用户登录失败”，联机丛书主题 [MSSQLSERVER_18456](../../relational-databases/errors-events/mssqlserver-18456-database-engine-error.md) 包含有关错误代码的其他信息。 Aaron Bertrand 的博客[故障排除错误 18456](http://www2.sqlblog.com/blogs/aaron_bertrand/archive/2011/01/14/sql-server-v-next-denali-additional-states-for-error-18456.aspx) 中提供了非常详细的错误代码列表。 你可以在对象资源管理器的“管理”部分中使用 SSMS（如果可以连接）查看错误日志。 否则，可以使用 Windows 记事本程序查看错误日志。 默认位置因版本而异，且可以在安装过程中更改。 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 的默认位置是 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\ERRORLOG`。  

4.   如果可以使用共享内存进行连接，请使用 TCP 测试连接。 你可以通过在名称前指定 **tcp:** 来强制建立 TCP 连接。 例如：

|连接到：|类型：|例如：|
|-----------------|---------------|-----------------|
|默认实例|tcp:计算机名称|tcp:ACCNT27|
|命名实例|tcp:计算机名称\实例名称|tcp:ACCNT27\PAYROLL|
  
如果可以使用共享内存进行连接，但不能使用 TCP 进行连接，则必须修复 TCP 问题。 最有可能的问题是未启用 TCP。 若要启用 TCP，请参阅上面的 **启用协议** 步骤。

5.   如果你的目标是使用非管理员帐户进行连接，那么一旦能以管理员身份连接后，请使用客户端应用程序将使用的 Windows 身份验证登录名或 SQL Server 身份验证登录名重新尝试进行连接。

## <a name="opening-a-port-in-the-firewall"></a>在防火墙中打开端口

从多年前的 Windows XP Service Pack 2 开始，便已打开 Windows 防火墙，用于阻止来自另一台计算机的连接。 若要从另一台计算机使用 TCP/IP 进行连接，则必须在 SQL Server 计算机上，将防火墙配置为允许连接到数据库引擎所使用的 TCP 端口。 如前所述，默认实例通常侦听 TCP 端口 1433。 如果具有命名实例，或者更改了默认值，则 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] TCP 端口可能侦听其他端口。 请参阅开头部分有关收集信息以确定端口的内容。  
如果要连接到命名实例或 TCP 端口 1433 以外的端口，则还必须为 SQL Server Browser 服务打开 UDP 端口 1434。 有关在 Windows 防火墙中打开端口的分步说明，请参阅 [为数据库引擎访问配置 Windows 防火墙](configure-a-windows-firewall-for-database-engine-access.md)。

## <a name="testing-the-connection"></a>测试连接

一旦可以在同一台计算机上使用 TCP 进行连接，就可以尝试从客户端计算机进行连接。 从理论上讲，你可以使用任何客户端应用程序，但为了避免增加复杂性，请在客户端上安装 SQL Server 管理工具，并使用 SQL Server Management Studio 进行尝试。

1. 在客户端计算机上，使用 SQL Server Management Studio 通过 IP 地址和 TCP 端口号（格式为“IP 地址,端口号”）尝试进行连接。 例如， **192.168.1.101,1433** 。如果无法连接，则可能出现了以下问题之一：

    * IP 地址的**Ping** 操作不起作用，表明出现了常规的 TCP 配置问题。 返回到 **测试 TCP/IP 连接**一节。 
    *   SQL Server 未侦听 TCP 协议。 返回到 **启用协议**一节。 
    *   SQL Server 正在侦听的端口不是你指定的端口。 返回到 **收集 SQL Server 实例的相关信息**一节。 
    *   SQL Server TCP 端口被防火墙阻止。 返回到 **在防火墙中打开端口**一节。


2. 可以使用 IP 地址和端口号进行连接之后，尝试使用不带端口号的 IP 地址进行连接。 对于默认实例，仅使用 IP 地址。 对于命名实例，则使用 IP 地址和实例名称，格式为“IP 地址\实例名称”，例如 **192.168.1.101\PAYROLL** 。如果无法连接，则可能出现了以下问题之一：

    *   如果你正在连接到默认实例，它可能正在侦听 TCP 端口 1433 以外的端口，并且客户端未尝试连接到正确的端口号。
    *   如果你正在连接到命名实例，则端口号未返回到客户端。  

这两个问题都与向客户端提供端口号的 SQL Server Browser 服务有关。 解决方案如下：

  * 启动 SQL Server Browser 服务。 返回到“收集 SQL Server 实例的相关信息”一节的第 1.d 节。
  * SQL Server Browser 服务被防火墙阻止。 请在防火墙中打开 UDP 端口 1434。 返回到 **在防火墙中打开端口**一节。 （请确保打开的是 UDP 端口，而非 TCP 端口。 这两个端口非常不同。）
  * UDP 端口 1434 信息被路由器阻止。 UDP 通信（用户数据报协议）未设计为可通过路由器。 这可以防止网络被低优先级的流量占满。 你也许可以将路由器配置为转发 UDP 流量，或者可以决定在连接时始终提供端口号。
  * 如果客户端计算机正在使用 Windows 7 或 Windows Server 2008（或更新的操作系统），UDP 流量可能会被客户端操作系统删除，因为来自服务器的响应会从所查询 IP 地址以外的 IP 地址返回。 这是一项安全功能，目的是阻止“宽松源映射”。 有关详细信息，请参阅联机丛书主题 **故障排除：超时时间已到** 的 [多个服务器 IP 地址](http://msdn.microsoft.com/library/ms190181.aspx)一节。 这篇文章来自 SQL Server 2008 R2，但大体内容仍然适用。 你也许可以将客户端配置为使用正确的 IP 地址，或者可以决定在连接时始终提供端口号。
     
3. 可以使用 IP 地址（对于命名实例，则为 IP 地址和实例名称）进行连接之后，尝试使用计算机名称（对于命名实例，则为计算机名称和实例名称）进行连接。 将 `tcp:` 放在计算机名称的前面，以强制建立 TCP/IP 连接。 例如，对于名为 `ACCNT27`的计算机上的默认实例，请使用 `tcp:ACCNT27` ；对于该计算机上名为 `PAYROLL`的命名实例，请使用 `tcp:ACCNT27\PAYROLL` 。如果可以使用 IP 地址进行连接，但不能使用计算机名称进行连接，则表明存在名称解析问题。 返回到 **测试 TCP/IP 连接**一节的第 4 节。

4. 可以使用强制实施 TCP 的计算机名称进行连接之后，尝试使用不强制实施 TCP 的计算机名称进行连接。 例如，对于默认实例，仅使用计算机名称，如 `CCNT27`；对于命名实例，使用计算机名称和实例名称，如 `ACCNT27\PAYROLL`。如果在强制实施 TCP 时可以连接，但在不强制实施 TCP 时无法连接，则表明客户端可能正在使用另一种协议（例如命名管道）。

    1. 在客户端计算机上，在 SQL Server 配置管理器的左窗格中展开“SQL Native Client 版本配置”，然后选择“客户端协议”。
    2. 在右窗格中，确保 TCP/IP 已启用。 如果 TCP/IP 处于禁用状态，请右键单击“TCP/IP”，然后单击“启用”。
    3. 确保 TCP/IP 的协议顺序编号小于命名管道（或较低版本上的 VIA）协议。 通常，应该将共享内存保留为顺序 1，TCP/IP 保留为顺序 2。 仅当客户端和 SQL Server 在同一台计算机上运行时，才使用共享内存。 将按顺序尝试所有已启用的协议，直到其中一个成功为止，只不过当连接不属于同一台计算机时，将跳过共享内存。 

