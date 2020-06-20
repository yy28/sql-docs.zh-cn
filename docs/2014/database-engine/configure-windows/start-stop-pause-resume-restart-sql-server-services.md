---
title: 启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f4b102c8fd81923d7386c8e556896e715311a07e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934768"
---
# <a name="start-stop-pause-resume-restart-the-database-engine-sql-server-agent-or-sql-server-browser-service"></a>启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务
  本主题介绍如何 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、命令提示符、或 PowerShell 中的**net**命令 [!INCLUDE[tsql](../../includes/tsql-md.md)] 来启动、停止、暂停、恢复或重新启动、代理或 Browser 服务。  
  
-   **开始之前：**  
  
    -   [这些服务是什么？](#Services)  
  
    -   [其他信息](#MoreInformation)  
  
    -   [安全性](#Security)  
  
-   **相关说明：**  
  
    -   [SQL Server 配置管理器](#SSCMProcedure)  
  
    -   [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [命令提示符窗口中的 net 命令](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="what-is-the-ssdenoversion-service-the-ssnoversion-agent-service-and-the-ssnoversion-browser-service"></a><a name="Services"></a> 什么是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服务、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件是作为 Windows 服务运行的可执行程序。 作为 Windows 服务运行的程序可以继续运行，而不在计算机屏幕上显示任何活动。  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)]服务**  
 作为 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的可执行进程。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可以是默认实例（每台计算机只有一个），也可以是多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)]命名实例中的一个。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器确定在计算机上安装哪些 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。 默认实例（如果安装）作为** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （MSSQLSERVER）** 列出。 命名实例（如果安装）将列为** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （<instance_name>）**。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 安装为** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （SQLEXPRESS）**。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理服务**  
 一种 Windows 服务，可执行计划的管理任务（称为作业和警报）。 有关详细信息，请参阅 [SQL Server Agent](../../ssms/agent/sql-server-agent.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关各个版本支持的功能列表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 服务**  
 一种 Windows 服务，可侦听对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源的传入请求并为客户端提供有关计算机中安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的信息。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务的单个实例用于计算机上安装的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
###  <a name="additional-information"></a><a name="MoreInformation"></a>附加信息  
  
-   暂停 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务将阻止新用户连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，但是已连接的用户可以继续工作到连接断开时为止。 当希望在您停止该服务前等待用户完成工作时，请使用“暂停”。 这使他们能够完成正在进行的事务。 “继续”允许 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 再次接受新连接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务不能暂停或继续。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用以下图标显示服务的当前状态。  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager**  
  
    -   服务名称旁边的图标上的绿色箭头表示服务已启动。  
  
    -   服务名称旁边的图标上的红色正方形表示服务已停止。  
  
    -   服务名称旁边的图标上的两条蓝色竖线表示服务已暂停。  
  
    -   重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)]时，将用红色正方形表示服务已停止，然后用绿色箭头表示服务已成功启动。  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   服务名称旁边的绿色圆圈图标上的白色箭头表示服务已启动。  
  
    -   服务名称旁边的红色圆圈图标上的白色正方形表示服务已停止。  
  
    -   服务名称旁边的蓝色圆圈图标上的两条白色竖线表示服务已暂停。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]时，只提供可能的选项。 例如，如果服务已启动， **“启动”** 将不可用。  
  
-   在群集上运行时， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服务最好使用群集管理器来管理。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 默认情况下，只有本地管理员组的成员能够启动、停止、暂停、继续或重新启动服务。 若要向管理员之外的用户授予管理服务的权限，请参阅 [如何授予用户管理 Windows Server 2003 中的服务的权限](https://support.microsoft.com/kb/325349)。 （此过程在其他 Windows 版本上是类似的。）  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] `SHUTDOWN` 命令停止需要**sysadmin**或**serveradmin**固定服务器角色的成员身份，并且不可转让。  
  
##  <a name="using-ssnoversion-configuration-manager"></a><a name="SSCMProcedure"></a> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-ssdenoversion"></a>启动、停止、暂停、继续或重新启动 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
2.  如果此时出现 **“用户帐户控制”** 对话框，请单击 **“是”** 。  
  
3.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器的左窗格中，单击 **“SQL Server 服务”**。  
  
4.  在结果窗格中，右键单击 **SQL Server (MSSQLServer)** 或某个命名实例，然后单击“启动”  、“停止”  、“暂停”  、“继续”  或“重启”  。  
  
5.  单击 **“确定”** 关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
> [!NOTE]  
>  若要使用启动选项启动一个 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例，请参阅[配置服务器启动选项（SQL Server 配置管理器）](scm-services-configure-server-startup-options.md)。  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-ssnoversion-browser-or-an-instance-of-the-ssnoversion-agent"></a>启动、停止、暂停、继续或重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理实例  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
2.  如果此时出现 **“用户帐户控制”** 对话框，请单击 **“是”** 。  
  
3.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器的左窗格中，单击 **“SQL Server 服务”**。  
  
4.  在结果窗格中，右键单击命名实例的 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浏览器**" 或 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理（MSSQLServer）** " 或 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理（<Instance_name>）** "，然后单击 "**启动**"、"**停止**"、"**暂停**"、"**恢复**" 或 "**重新启动**"。  
  
5.  单击 **“确定”** 关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理不能暂停。  
  
##  <a name="using-ssnoversion-management-studio"></a><a name="SSMSProcedure"></a> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-ssdenoversion"></a>启动、停止、暂停、继续或重新启动 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，右键单击要启动的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后单击“启动”****、“停止”****、“暂停”****、“继续”**** 或“重启”****。  
  
     或者，在“已注册的服务器”中，右键单击要启动的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，指向“服务控制”****，然后单击“启动”****、“停止”****、“暂停”****、“继续”**** 或“重启”****。  
  
2.  如果此时出现 **“用户帐户控制”** 对话框，请单击 **“是”** 。  
  
3.  系统提示是否要执行该操作时，请单击 **“是”**。  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-ssnoversion-agent"></a>启动、停止或重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理实例  
  
1.  在对象资源管理器中，连接到的实例 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，右键单击 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理**"，然后单击 "**启动**"、"**停止**" 或 "**重新启动**"。  
  
2.  如果此时出现 **“用户帐户控制”** 对话框，请单击 **“是”** 。  
  
3.  系统提示是否要执行该操作时，请单击 **“是”**。  
  
##  <a name="from-the-command-prompt-window-using-net-commands"></a><a name="CommandPrompt"></a>在命令提示符窗口中使用 net 命令  
 可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows net 命令启动、停止或暂停 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务****。  
  
###  <a name="to-start-the-default-instance-of-the-ssde"></a><a name="dbDefault"></a>启动的默认实例[!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   在命令提示符下，输入下列命令之一：  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     \- 或 -  
  
     **net start MSSQLSERVER**  
  
###  <a name="to-start-a-named-instance-of-the-ssde"></a><a name="dbNamed"></a> 启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   在命令提示符下，输入下列命令之一。 替换 *\<instancename>* 为要管理的实例的名称。  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     \- 或 -  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="to-start-the-ssde-with-startup-options"></a><a name="dbStartup"></a> 使用启动选项启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   将启动选项添加到 **net start "SQL Server (MSSQLSERVER)"** 语句末尾，之间用空格分隔开。 使用 **net start**启动时，启动选项使用正斜杠 (/) 而不是连字符 (-)。  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     -或-  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  有关启动选项的详细信息，请参阅 [数据库引擎服务启动选项](database-engine-service-startup-options.md)。  
  
###  <a name="to-start-the-ssnoversion-agent-on-the-default-instance-of-ssnoversion"></a><a name="agDefault"></a> 使用启动选项启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认实例上启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   在命令提示符下，输入下列命令之一：  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     \- 或 -  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="to-start-the-ssnoversion-agent-on-a-named-instance-of-ssnoversion"></a><a name="agNamed"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在的命名实例上启动代理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   在命令提示符下，输入下列命令之一。 将 *instancename* 替换为要管理的实例的名称。  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     \- 或 -  
  
     **net start SQLAgent$** *instancename*  
  
 有关如何在详细模式中运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以执行故障排除的信息，请参阅 [sqlagent90 应用程序](../../tools/sqlagent90-application.md)。  
  
###  <a name="to-start-the-ssnoversion-browser"></a><a name="Browser"></a>启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浏览器  
  
-   在命令提示符下，输入下列命令之一：  
  
     **net start "SQL Server Browser"**  
  
     -或-  
  
     **net start SQLBrowser**  
  
###  <a name="to-pause-or-stop-services-from-the-command-prompt-window"></a><a name="pauseStop"></a> 在命令提示符窗口中暂停或停止服务  
  
-   要暂停或停止服务，请通过以下方式修改命令：  
  
    -   若要暂停服务，请将 **net start** 替换为 **net pause**。  
  
    -   若要停止服务，请将 **net start** 替换为 **net stop**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用 `SHUTDOWN` 语句停止[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
#### <a name="to-stop-the-ssde-using-tsql"></a>使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 停止 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   要等待当前运行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和存储过程完成后停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，请执行以下语句：  
  
    ```sql  
    SHUTDOWN;   
    ```  
  
-   要立即停止[!INCLUDE[ssDE](../../includes/ssde-md.md)]，请执行以下语句：  
  
    ```sql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 有关语句的详细信息 `SHUTDOWN` ，请参阅[SHUTDOWN &#40;transact-sql&#41;](/sql/t-sql/language-elements/shutdown-transact-sql)。  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
  
#### <a name="to-start-and-stop-ssde-services"></a>启动和停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务  
  
1.  在命令提示符窗口中，通过执行以下命令启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell：  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 命令提示符下，执行以下命令。 使用您的计算机名称替换 `computername` 。  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (Get-Item .).ManagedComputer
    ```  
  
3.  标识要停止或启动的服务。 选取下列行之一。 使用命名实例的名称替换 `instancename` 。  
  
    -   获取对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]默认实例的引用。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   获取对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]命名实例的引用。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   获取对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认实例上 [!INCLUDE[ssDE](../../includes/ssde-md.md)]代理服务的引用。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   获取对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例上 [!INCLUDE[ssDE](../../includes/ssde-md.md)]代理服务的引用。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   获取对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务的引用。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  完成示例以启动然后停止所选服务。  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [以最小配置启动 SQL Server](start-sql-server-with-minimal-configuration.md)   
 [SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
