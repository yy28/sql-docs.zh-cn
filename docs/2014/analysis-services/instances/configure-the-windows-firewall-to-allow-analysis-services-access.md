---
title: 配置 Windows 防火墙以允许 Analysis Services 访问 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ports [Analysis Services]
- Windows Firewall [Analysis Services]
- firewall systems [Analysis Services]
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c5066a27097bb0919a6d0af0ffa9ad1c53e8624
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730372"
---
# <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a>将 Windows 防火墙配置为允许 Analysis Services 访问
  使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 可在网络上使用的至关重要的第一步是确定您是否需要在防火墙中取消阻止端口。 大多数安装都要求您至少创建一个允许连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的入站防火墙规则。  
  
 根据您安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的方式，防火墙配置要求会有所不同。  
  
-   在安装默认实例或创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 故障转移群集时，请打开 TCP 端口 2383。  
  
-   在安装命名实例时打开 TCP 端口 2382。 命名实例使用动态端口分配。 作为 Analysis Services 的发现服务，SQL Server Browser 服务侦听 TCP 端口 2382 并将连接请求重定向到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]当前使用的端口。  
  
-   在 SharePoint 模式下安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 时请打开 TCP 端口 2382，以支持 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013。 在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例是 SharePoint 的外部实例。 对名为“PowerPivot”实例的入站请求是由 SharePoint Web 应用程序通过网络连接生成的，需要一个开放端口。 与其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 命名实例一样，针对 TCP 2382 为 SQL Server Browser 服务创建一个入站规则以允许访问 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。  
  
-   对于 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010，请勿在 Windows 防火墙中开放端口。 作为 SharePoint 的外接程序，该服务使用为 SharePoint 配置的端口并且仅与加载和查询 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据模型的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 实例建立本地连接。  
  
-   对于运行在 Windows Azure 虚拟机上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，请使用其他说明来配置服务器访问。 请参阅 [Windows Azure 虚拟机中的 SQL Server 商业智能](https://msdn.microsoft.com/library/windowsazure/jj992719.aspx)。  
  
 尽管的默认实例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]侦听 TCP 端口 2383年，但你可以配置服务器以侦听其他固定端口，连接到此格式中的服务器：\<服务器名 >:\<端口号 >。  
  
 一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例只能使用一个 TCP 端口。 在具有多个网卡或多个 IP 地址的计算机上， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在一个 TCP 端口上侦听分配给或化名为该计算机的所有 IP 地址。 如果您有特定多端口要求，请考虑配置 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以实现 HTTP 访问。 然后您可以在选择的任意端口上设置多个 HTTP 端点。 请参阅[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
 本主题包含以下各节：  
  
-   [检查 Analysis Services 的端口和防火墙设置。](#bkmk_checkport)  
  
-   [为 Analysis Services 的默认实例配置 Windows 防火墙](#bkmk_default)  
  
-   [为 Analysis Services 的命名实例配置 Windows 防火墙访问](#bkmk_named)  
  
-   [Analysis Services 群集的端口配置](#bkmk_cluster)  
  
-   [Powerpivot for SharePoint 的端口配置](#bkmk_powerpivot)  
  
-   [将固定端口用于 Analysis Services 的默认实例或命名实例](#bkmk_fixed)  
  
 有关默认 Windows 防火墙设置的详细信息以及有关影响数据库引擎、Analysis Services、Reporting Services 和 Integration Services 的 TCP 端口的说明，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
##  <a name="bkmk_checkport"></a> 检查 Analysis Services 的端口和防火墙设置。  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]支持的 Microsoft Windows 操作系统上，Windows 防火墙默认处于打开状态并阻止远程连接。 必须手动在防火墙中开放某一端口，以便允许对 Analysis Services 的入站请求。 SQL Server 安装程序不自动为您执行此步骤。  
  
 在 msmdsrv.ini file 文件以及 SQL Server Management Studio 的 Analysis Services 实例的“常规”属性页中，指定端口设置。 如果 `Port` 设置为某个正整数，则该服务正在侦听某个固定端口。 如果 `Port` 设置为 0，则该服务正在侦听端口 2383（如果该服务是默认实例）或动态分配的端口（如果该服务是命名实例）。  
  
 动态端口分配仅由命名实例使用。 `MSOLAP$InstanceName` 服务确定在它启动时要使用的端口。 您可以通过执行以下操作确定某一命名实例正在使用的实际端口号：  
  
-   启动任务管理器，然后单击**Services**若要获取的 PID `MSOLAP$InstanceName`。  
  
-   从命令行运行 `netstat -ao -p TCP`，以便查看该 PID 的 TCP 端口信息。  
  
-   通过使用 SQL Server Management Studio 验证该端口，并连接到 Analysis Services 服务器按以下格式：\<Ip 地址 >:\<端口号 >。  
  
 尽管应用程序可能在侦听某一特定端口，但如果防火墙正在阻止访问，则连接将不会成功。 为了实现与某一命名 Analysis Services 实例的连接，您必须取消阻止对 msmdsrv.exe 或者该实例在防火墙中所侦听的固定端口的访问。 本主题中的其余部分将说明如何取消阻止。  
  
 若要查看是否已为 Analysis Services 定义了防火墙设置，请在“控制面板”中使用“高级安全 Windows 防火墙”。 “监视”文件夹的“防火墙”页显示为本地服务器定义的规则的完整列表。  
  
 请注意，对于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，必须手动定义所有防火墙规则。 尽管 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 SQL Server Browser 保留端口 2382 和 2383，但 SQL Server 安装程序以及任何配置工具都不会定义允许访问这些端口或程序可执行文件的防火墙规则。  
  
##  <a name="bkmk_default"></a> 为 Analysis Services 的默认实例配置 Windows 防火墙  
 默认的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例侦听 TCP 端口 2383。 如果您安装了默认实例并且想要使用此端口，则仅需在 Windows 防火墙中取消阻止对 TCP 端口 2383 的入站访问，以便允许远程访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的默认实例。 如果您安装了该默认实例，但是想要将服务配置为侦听固定端口，请参阅本主题中的 [将固定端口用于 Analysis Services 的默认实例或命名实例](#bkmk_fixed) 。  
  
 若要确认该服务是否正作为默认实例 (MSSQLServerOLAPService) 运行，请在 SQL Server 配置管理器中查看服务名称。 Analysis Services 的默认实例始终作为“SQL Server Analysis Services (MSSQLSERVER)”列出。  
  
> [!NOTE]  
>  不同的 Windows 操作系统为配置 Windows 防火墙提供可供选择的工具。 其中大多数工具都允许您在打开特定端口还是程序可执行文件之间进行选择。 除非您有具体原因来指定程序可执行文件，否则，我们建议您指定端口。  
  
 在指定入站规则时，请确保采用使你以后能够轻松找到规则的命名约定（例如 **SQL Server Analysis Services (TCP-in) 2383**）。  
  
#### <a name="windows-firewall-with-advanced-security"></a>高级安全 Windows 防火墙  
  
1.  在 Windows 7 或 Windows Vista 上，单击“控制面板”中的 **“系统和安全”**，选择 **“Windows 防火墙”**，然后单击 **“高级设置”**。 在 Windows Server 2008 或 2008 R2 上，打开“管理员工具”，然后单击 **“高级安全 Windows 防火墙”**。 在 Windows Server 2012 上，打开“应用程序”页并键入 **Windows 防火墙**。  
  
2.  右键单击“入站规则”，然后选择“新建规则”。  
  
3.  在规则类型中单击`Port`，然后单击**下一步**。  
  
4.  在协议和端口，选择**TCP** ，然后键入`2383`中**特定本地端口**。  
  
5.  在“操作”中，单击 **“允许连接”** ，然后单击 **“下一步”**。  
  
6.  在“配置文件”中，清除不适用的所有网络位置，然后单击 **“下一步”**。  
  
7.  在名称中，键入此规则的说明性名称 (例如， `SQL Server Analysis Services (tcp-in) 2383`)，然后单击**完成**。  
  
8.  若要确认远程连接已启用，请在另一台计算机上打开 SQL Server Management Studio 或 Excel，然后通过在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] “服务器名称” **中指定服务器的网络名称来连接到**。  
  
    > [!NOTE]  
    >  在您授予权限前，其他用户将无权访问此服务器。 有关详细信息，请参阅[授予对对象和操作的访问权限 (Analysis Services)](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)。  
  
#### <a name="netsh-advfirewall-syntax"></a>Netsh AdvFirewall 语法  
  
-   下面的命令创建一个入站规则，该规则允许 TCP 端口 2383 上的传入请求。  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> 为 Analysis Services 的命名实例配置 Windows 防火墙访问  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的命名实例可侦听固定端口或动态分配的端口，其中，SQL Server Browser 服务提供在连接时对服务而言是最新的连接信息。  
  
 SQL Server Browser 服务侦听 TCP 端口 2382。 不使用 UDP。 TCP 是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]使用的唯一传输协议。  
  
 选择以下方法之一可以启用对 Analysis Services 的命名实例的远程访问：  
  
-   使用动态端口分配和 SQL Server Browser 服务。 在 Windows 防火墙中取消阻止 SQL Server Browser 服务使用的端口。 连接到服务器按以下格式：\<服务器名称 >\\< 实例名\>。  
  
-   一起使用固定端口和 SQL Server Browser 服务。 此方法可让你连接使用此格式：\<服务器名称 >\\< 实例名\>，不同之处在于服务器侦听固定端口的这种情况下，动态端口分配方法相同。 在此方案中，SQL Server Browser 服务提供对在固定端口上侦听的 Analysis Services 实例的名称解析。 若要使用此方法，请将服务器配置为侦听固定端口，取消阻止对该端口的访问，并且取消阻止对 SQL Server Browser 服务使用的端口的访问。  
  
 SQL Server Browser 服务仅用于命名实例，不能用于默认实例。 只要您将任何 SQL Server 功能作为命名实例安装，就将自动安装和启用该服务。 如果您选择要求 SQL Server Browser 服务的方法，请确保该服务在您的服务器上保持启用和启动。  
  
 如果无法使用 SQL Server Browser 服务，则必须在连接字符串中分配固定端口，绕过域名解析。 没有 SQL Server Browser 服务，所有客户端连接都必须在连接字符串上包括端口号（例如 AW-SRV01:54321）。  
  
 **选项 1:使用动态端口分配并且取消阻止对 SQL Server Browser 服务的访问**  
  
 在服务启动时由 `MSOLAP$InstanceName` 建立对 Analysis Services 的命名实例的端口分配。 默认情况下，该服务声明它找到的第一个可用端口号，并且在该服务每次重新启动时都使用不同的端口号。  
  
 实例名称解析由 SQL Server Browser 服务处理。 如果您在将动态端口分配用于命名实例，则始终要求为 SQL Server Browser 服务取消阻止 TCP 端口 2382。  
  
> [!NOTE]  
>  SQL Server Browser 服务分别为数据库引擎和 Analysis Services 侦听 UDP 端口 1434 和 TCP 端口 2382。 即使您已经为 SQL Server Browser 服务取消阻止了 UDP 端口 1434，也仍然必须为 Analysis Services 取消阻止 TCP 端口 2382。  
  
#### <a name="windows-firewall-with-advanced-security"></a>高级安全 Windows 防火墙  
  
1.  在 Windows 7 或 Windows Vista 上，单击“控制面板”中的 **“系统和安全”**，选择 **“Windows 防火墙”**，然后单击 **“高级设置”**。 在 Windows Server 2008 或 2008 R2 上，打开“管理员工具”，然后单击 **“高级安全 Windows 防火墙”**。 在 Windows Server 2012 上，打开“应用程序”页并键入 **Windows 防火墙**。  
  
2.  若要取消阻止对 SQL Server Browser 服务的访问，请右键单击“入站规则”，然后选择“新建规则”。  
  
3.  在规则类型中单击`Port`，然后单击**下一步**。  
  
4.  在协议和端口，选择**TCP** ，然后键入`2382`中**特定本地端口**。  
  
5.  在“操作”中，单击 **“允许连接”** ，然后单击 **“下一步”**。  
  
6.  在“配置文件”中，清除不适用的所有网络位置，然后单击 **“下一步”**。  
  
7.  在名称中，键入此规则的说明性名称 (例如， `SQL Server Browser Service (tcp-in) 2382`)，然后单击**完成**。  
  
8.  若要确认远程连接已启用，另一台计算机上打开 SQL Server Management Studio 或 Excel 并连接到 Analysis Services 通过按以下格式指定服务器的网络名称和实例名称：\<服务器名 >\\< 实例名\>。 例如，在具有 **Finance** 的命名实例的名为 **AW-SRV01** 的服务器上，服务器名称为 **AW-SRV01\Finance**。  
  
 **选项 2:将固定的端口用于命名实例**  
  
 或者，您可以分配一个固定端口，然后取消阻止对该端口的访问。 与允许访问程序可执行文件的方法相比，此方法可提高审核功能。 因此，建议使用固定端口来访问所有 Analysis Services 实例。  
  
 若要分配固定端口，请按照本主题的 [将固定端口用于 Analysis Services 的默认实例或命名实例](#bkmk_fixed) 中的说明执行，然后返回到本节以便取消阻止该端口。  
  
#### <a name="windows-firewall-with-advanced-security"></a>高级安全 Windows 防火墙  
  
1.  在 Windows 7 或 Windows Vista 上，单击“控制面板”中的 **“系统和安全”**，选择 **“Windows 防火墙”**，然后单击 **“高级设置”**。 在 Windows Server 2008 或 2008 R2 上，打开“管理员工具”，然后单击 **“高级安全 Windows 防火墙”**。 在 Windows Server 2012 上，打开“应用程序”页并键入 **Windows 防火墙**。  
  
2.  若要取消阻止对 Analysis Services 的访问，请右键单击“入站规则”，然后选择“新建规则”。  
  
3.  在规则类型中单击`Port`，然后单击**下一步**。  
  
4.  在“协议和端口”中，选择 **“TCP”** ，然后在 **“特定本地端口”** 中键入固定端口。  
  
5.  在“操作”中，单击 **“允许连接”** ，然后单击 **“下一步”**。  
  
6.  在“配置文件”中，清除不适用的所有网络位置，然后单击 **“下一步”**。  
  
7.  在名称中，键入此规则的说明性名称 (例如， `SQL Server Analysis Services on port 54321`)，然后单击**完成**。  
  
8.  若要确认远程连接已启用，另一台计算机上打开 SQL Server Management Studio 或 Excel，并通过按以下格式指定服务器和端口号的网络名称连接到 Analysis Services:\<服务器名 >:\<端口号 >。  
  
#### <a name="netsh-advfirewall-syntax"></a>Netsh AdvFirewall 语法  
  
-   下面的命令创建两个入站规则；一个规则为 SQL Server Browser 服务取消阻止 TCP 2382，另一个规则取消阻止您为 Analysis Services 实例指定的固定端口。 您可以运行这两个规则中的一个以便允许访问 Analysis Services 实例。  
  
     在这个示例命令中，端口 54321 是固定端口。 请确保用在您的系统上使用的实际端口替换此端口。  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> 将固定端口用于 Analysis Services 的默认实例或命名实例  
 本节说明如何配置 Analysis Services 以便侦听固定端口。 如果您将 Analysis Services 作为命名实例安装，则使用固定端口较为常见；但是，如果业务或安全要求指定您使用非默认端口分配，则也可以使用此方法。  
  
 请注意，使用固定端口将通过要求您将端口号追加到服务器名称后，更改默认实例的连接语法。 例如，在连接到在 SQL Server Management Studio 中侦听端口 54321 的本地默认 Analysis Services 实例时，将要求您在 Management Studio 的“连接到服务器”对话框中键入 localhost:54321 作为服务器名称。  
  
 如果使用的命名的实例，可以将固定的端口，无需更改分配到指定服务器名称的方式 (具体而言，可以使用\<servername\instancename > 若要连接到侦听固定端口的命名实例)。 这仅适用于 SQL Server Browser 服务正在运行并且您已取消阻止了该服务正在侦听的端口的情况。 SQL Server Browser 服务将提供重定向到基于的固定端口\<servername\instancename >。 只要您为 SQL Server Browser 服务以及侦听固定端口的 Analysis Services 的命名实例开放端口，SQL Server Browser 服务就会解析与命名实例的连接。  
  
1.  确定要使用的可用 TCP/IP 端口。  
  
     若要查看应避免使用的保留和已注册端口的列表，请参阅 [端口号 (IANA)](https://go.microsoft.com/fwlink/?LinkID=198469)。 若要查看在您的系统上已使用端口的列表，请打开命令提示符窗口，然后键入 `netstat -a -p TCP` 以便显示已在系统上打开的 TCP 端口的列表。  
  
2.  在您确定了要使用的端口后，通过在 msmdsrv.ini 文件中或者在 SQL Server Management Studio 的 Analysis Services 实例的“常规属性”页中编辑 `Port` 配置设置，指定该端口。  
  
3.  重新启动服务。  
  
4.  配置 Windows 防火墙以便取消阻止您指定的 TCP 端口。 或者，如果您在将固定端口用于命名实例，则取消阻止您为该实例指定的 TCP 端口以及为 SQL Server Browser 服务指定的 TCP 端口 2382。  
  
5.  通过先进行本地连接（在 Management Studio 中），然后从其他计算机上的客户端应用程序进行远程连接，进行验证。 若要使用 Management Studio，连接到 Analysis Services 默认实例通过按以下格式指定服务器名称：\<服务器名 >:\<端口号 >。 对于命名实例，指定服务器名称，例如\<服务器名称 >\\< 实例名\>。  
  
##  <a name="bkmk_cluster"></a> Analysis Services 群集的端口配置  
 无论安装为默认实例还是命名实例， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 故障转移群集始终在 TCP 端口 2383 上进行侦听。 安装在 Windows 故障转移群集上时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不使用动态端口分配。 请务必在群集中运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的所有节点上开放 TCP 2383。 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]群集的详细信息，请参阅 [如何安装群集 SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548)。  
  
##  <a name="bkmk_powerpivot"></a> Powerpivot for SharePoint 的端口配置  
 根据您使用的 SharePoint 版本， [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 的服务器体系结构会有本质区别。  
  
 **SharePoint 2013**  
  
 在 SharePoint 2013 中，Excel Services 会重定向对 Power Pivot 数据模型的请求，这些模型随后将在 SharePoint 环境外部的某一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上加载。 连接遵循通常的模式，在该模式下，本地计算机上的 Analysis Services 客户端库向同一网络中的远程 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例发送连接请求。  
  
 因为 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 始终将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安装为命名实例，所以您应采用 SQL Server Browser 服务和动态端口分配。 如前所述，SQL Server Browser 服务在 TCP 端口 2382 上侦听发送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 命名实例的连接请求，并将该请求重定向到当前端口。  
  
 请注意，SharePoint 2013 中的 Excel Services 不支持固定端口连接语法，因此请确保 SQL Server Browser 服务可以访问。  
  
 **SharePoint 2010**  
  
 如果您使用的是 SharePoint 2010，则无需在 Windows 防火墙中开放端口。 SharePoint 会开放它所需的端口，并且诸如 PowerPivot for SharePoint 的外接程序可以在 SharePoint 环境中运行。 在 PowerPivot for SharePoint 2010 安装中，PowerPivot 系统服务独占使用与其安装在同一台计算机上的本地 SQL Server Analysis Services (PowerPivot) 服务实例。 它使用本地连接（而非网络连接）来访问加载、查询和处理 SharePoint 服务器上的 PowerPivot 数据的本地 Analysis Services 引擎服务。 若要从客户端应用程序请求 PowerPivot 数据，请求进行路由通过 SharePoint 安装程序开放的端口 (具体而言，定义入站的规则以允许访问 SharePoint-80，SharePoint 管理中心 v4，SharePoint Web 服务和 SPUserCodeV4)。 因为 PowerPivot Web 服务在 SharePoint 场内运行，所以，SharePoint 防火墙规则足以用于远程访问 SharePoint 场中的 PowerPivot 数据了。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Browser 服务（数据库引擎和 SSAS）](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  
