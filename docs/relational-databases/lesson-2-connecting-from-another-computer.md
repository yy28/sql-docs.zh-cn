---
title: 第 2 课：从其他计算机进行连接 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 615aa894b7ceb07d471c281eb6be24db9c0e3a43
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657567"
---
# <a name="lesson-2-connecting-from-another-computer"></a>第 2 课：从其他计算机进行连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
为了增强安全性， [!INCLUDE[ssDE](../includes/ssde-md.md)] Developer Edition、Express Edition 和 Evaluation Edition 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在初始安装时不能从其他计算机对其进行访问。 本课介绍如何启用协议，配置端口以及配置 Windows 防火墙，以便从其他计算机进行连接。  
  
本课程包含以下任务：  
  
-   [启用协议](#protocols)  
  
-   [配置固定端口](#port)  
  
-   [打开防火墙的端口](#firewall)  
  
-   [从其他计算机连接到数据库引擎](#otherComp)  
  
-   [使用 SQL Server Browser 服务进行连接](#browser)  
  
## <a name="protocols"></a>启用协议  
为了增强安全性， [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]、Developer 和 Evaluation 仅安装有限的网络连接。 可以通过运行同一台计算机的工具建立到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的连接，但是不能从其他计算机进行连接。 如果您计划在 [!INCLUDE[ssDE](../includes/ssde-md.md)]所在的那台计算机上执行您的开发工作，则不必启用附加协议。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 将通过使用 Shared Memory 协议连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 。 此协议已经启用。  
  
如果计划从其他计算机连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] ，则必须启用一个协议，例如 TCP/IP。  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>如何从其他计算机启用 TCP/IP 连接  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”**、 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]、 **“配置工具”**，然后单击 **“SQL Server 配置管理器”**。  
  
    > [!NOTE]  
    > 您可能同时拥有 32 位和 64 位选项。  
  
    > [!NOTE]  
    > 因为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。 文件名包含表示 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本号的数字。 若要从“运行”命令打开配置管理器，以下是在 C 驱动器上安装 Windows 时最后四个版本的路径。  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
2.  在“SQL Server 配置管理器”中，展开“SQL Server 网络配置”，然后单击“*<InstanceName>* 的”。  
  
    默认实例（未命名实例）作为 **MSSQLSERVER** 列出。 如果您已经安装了某个命名实例，则您提供的名称将会列出。 [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] 作为 **SQLEXPRESS**安装，除非你在安装过程中更改了该名称。  
  
3.  在协议列表中，右键单击要启用的协议 (**TCP/IP**)，再单击“启用”。  
  
    > [!NOTE]  
    > 对网络协议进行更改后，必须重新启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服务；但此操作是在下一任务中完成的。  
  
## <a name="port"></a>配置固定端口  
为了增强安全性，Windows Server 2008、 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]和 Windows 7 均打开了 Windows 防火墙。 在您从其他计算机连接到此实例时，必须打开防火墙中的通信端口。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的默认实例侦听端口 1433；因此，您不需要配置固定端口。 不过，包括 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 的命令实例会侦听动态端口。 打开防火墙的端口之前，必须首先将 [!INCLUDE[ssDE](../includes/ssde-md.md)] 配置为侦听特定端口（称为固定端口或静态端口）；否则， [!INCLUDE[ssDE](../includes/ssde-md.md)] 可能会在每次启动时侦听不同的端口。 有关防火墙、默认 Windows 防火墙设置的详细信息以及有关影响数据库引擎、Analysis Services、Reporting Services 和 Integration Services 的 TCP 端口的说明，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
> [!NOTE]  
> Internet 号码分配机构负责管理端口号的分配，并在 [https://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844) 上列出这些端口号。应分配的端口号的范围是从 49152 到 65535。  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>配置 SQL Server 以侦听特定端口  
  
1.  在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器中，展开“SQL Server 网络配置”，然后单击要配置的服务器实例。  
  
2.  在右窗格中，双击 **TCP/IP**。  
  
3.  在“TCP/IP 属性”对话框中，单击“IP 地址”选项卡。  
  
4.  在 **IPAll** 部分的“TCP 端口”框中，键入可用的端口号。 对于本教程，我们将使用 **49172**。  
  
5.  单击“确定”关闭对话框，然后单击表明必须重新启动服务的警告上的“确定”。  
  
6.  在左窗格中，单击 **“SQL Server 服务”**。  
  
7.  在右窗格中，右键单击 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，再单击“重新启动”。 当 [!INCLUDE[ssDE](../includes/ssde-md.md)] 重新启动时，它将侦听端口 **49172**。  
  
## <a name="firewall"></a>打开防火墙的端口  
防火墙系统有助于阻止对计算机资源进行未经授权的访问。 若要在防火墙打开时从其他计算机连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，必须打开防火墙的端口。  
  
> [!IMPORTANT]  
> 打开防火墙的端口可能会使服务器受到恶意攻击。 请确保在打开端口之前了解防火墙系统。 有关详细信息，请参阅 [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
将 [!INCLUDE[ssDE](../includes/ssde-md.md)] 配置为使用固定端口后，请按照下列说明在 Windows 防火墙中打开该端口。 （您不需要为默认实例配置固定端口，因为它已经具有固定的 TCP 端口 1433。）  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>打开 Windows 防火墙的端口以进行 TCP 访问 (Windows 7)  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**，键入 **WF.msc**，然后单击 **“确定”**。  
  
2.  在“高级安全 Windows 防火墙”的左窗格中，右键单击“入站规则”，然后在操作窗格中单击“新建规则”。  
  
3.  在 **“规则类型”** 对话框中，选择 **“端口”**，然后单击 **“下一步”**。  
  
4.  在 **“协议和端口”** 对话框中，选择 **TCP**。 选择“特定本地端口”，然后键入 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例的端口号。 为默认实例键入 1433。 如果要配置命名实例，并在上一个任务中配置了固定端口，则键入 **49172**。 单击“下一步” 。  
  
5.  在 **“操作”** 对话框中，选择 **“允许连接”**，然后单击 **“下一步”**。  
  
6.  在 **“配置文件”** 对话框中，选择在您想要连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]时描述计算机连接环境的任何配置文件，然后单击 **“下一步”**。  
  
7.  在 **“名称”** 对话框中，输入此规则的名称和说明，再单击 **“完成”**。  
  
有关配置防火墙，包括 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]说明的详细信息，请参阅 [为数据库引擎访问配置 Windows 防火墙](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。 有关默认 Windows 防火墙设置的详细信息以及有关影响数据库引擎、Analysis Services、Reporting Services 和 Integration Services 的 TCP 端口的说明，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="otherComp"></a>从其他计算机连接到数据库引擎  
既然已配置 [!INCLUDE[ssDE](../includes/ssde-md.md)] 侦听固定端口，并且已在防火墙中打开该端口，您就可以从其他计算机连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 了。  
  
当 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务正在服务器计算机中运行并且防火墙已打开 UDP 端口 1434 时，可以使用计算机名称和实例名称建立连接。 为了增强安全性，我们的示例不使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务。  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>从其他计算机连接到数据库引擎  
  
1.  在另一台包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 客户端工具的计算机中，使用授权的帐户进行登录以连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，然后打开 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
2.  在“连接到服务器”对话框中，确认是否已在“服务器类型”框中选中“数据库引擎”。  
  
3.  在“服务器名称”框中，键入 **tcp:** 以便指定协议，后跟计算机名称、逗号以及端口号。 为了连接到默认实例，端口 1433 为隐式端口并可省略；因此，请键入 tcp:<computer_name>。 在命名实例的示例中，请键入 tcp:<computer_name>,49172****。  
  
    > [!NOTE]  
    > 如果你在“服务器名称”框中省略 **tcp:**，则客户端将按照在客户端配置中指定的顺序依次尝试所有启用的协议。  
  
4.  在“身份验证”框中，确认已选中“Window 身份验证”，然后单击“连接”。  
  
## <a name="browser"></a>使用 SQL Server Browser 服务进行连接  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务侦听对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 资源的传入请求，并提供有关计算机中安装的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的信息。 当 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务运行时，用户可以通过提供计算机名称和实例名（而不是计算机名称和端口号）连接到命名实例。 由于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 会接收未经身份验证的 UDP 请求，因此，不会在安装过程中始终处于打开状态。 有关该服务及其启用时间的说明，请参阅 [SQL Server Browser 服务（数据库引擎和 SSAS）](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)。  
  
若要使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser，必须按照本课之前的步骤执行，并打开防火墙的 UDP 端口 1434。  
  
此有关基本连接的简短教程将以此步骤为结束。  
  
## <a name="return-to-tutorials-portal"></a>返回到教程入门  
[教程：数据库引擎入门](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

