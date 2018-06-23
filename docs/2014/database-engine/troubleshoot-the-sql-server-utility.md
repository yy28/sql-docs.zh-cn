---
title: SQL Server 实用工具故障排除 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f5f47c2a-38ea-40f8-9767-9bc138d14453
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0bc94d8644d1a0015829b730d5556b967c6b8c93
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027514"
---
# <a name="troubleshoot-the-sql-server-utility"></a>SQL Server 实用工具故障排除
  解决 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具问题可能包括解决向 UCP 注册 SQL Server 实例的失败的操作、排除导致 UCP 上托管实例列表视图中图标灰显的失败的数据收集故障、缓解性能瓶颈或者解决资源运行状况问题。 有关缓解标识的资源运行状况问题的详细信息[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]UCP，请参阅[解决 SQL Server 资源运行状况&#40;SQL Server 实用工具&#41;](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)。  
  
## <a name="failed-operation-to-enroll-an-instance-of-sql-server-into-a-sql-server-utility"></a>向 SQL Server 实用工具中注册 SQL Server 实例的失败的操作  
 如果你连接到的实例[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用注册[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证，并且指定属于与 UCP 所在的域不同的 Active Directory 域的代理帐户实例验证将成功，但注册操作将失败并显示以下错误消息：  
  
 执行 Transact-SQL 语句或批处理时发生了异常。 (Microsoft.SqlServer.ConnectionInfo)  
  
 其他信息: 无法获取有关 Windows NT 组/用户 '\<DomainName\AccountName>' 的信息，错误代码 0x5。 （Microsoft SQL Server，错误：15404）  
  
 在以下示例中将发生此问题：  
  
1.  UCP 是“Domain_1”的成员。  
  
2.  存在单向域信任关系：即，“Domain_1”不为“Domain_2”所信任，但“Domain_2”为“Domain_1”所信任。  
  
3.  要注册到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例还是“Domain_1”的成员。  
  
4.  在该注册操作过程中，使用“sa”连接到要注册的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例。 指定来自“Domain_2”的一个代理帐户。  
  
5.  验证成功但注册失败。  
  
 上面的示例针对此问题的解决方法是使用“sa”连接到要注册到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实用工具中的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，并且提供来自“Domain_1”的一个代理帐户。  
  
## <a name="failed-wmi-validation"></a>失败的 WMI 验证  
 如果在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例上未正确配置 WMI，则“创建 UCP”和“注册托管实例”操作将显示一个警告，但不阻塞该操作。 此外，如果你更改[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理帐户配置，以便[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理没有所需的 WMI 类，受影响托管实例上的数据收集到的权限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]无法上载到 UCP。 这将导致 UCP 中的灰色图标。  
  
 失败的数据收集将导致 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的受影响托管实例的 UCP 列表视图中的灰色状态图标。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例上的作业历史记录显示 sysutility_mi_collect_and_upload 在步骤 2（暂存从 PowerShell 脚本收集的数据）上失败。  
  
 简化的错误消息如下：  
  
 命令执行已停止，因为 shell 变量 "ErrorActionPreference" 设置为 Stop: 拒绝访问。  
  
 错误：\<日期-时间 （MM/DD/YYYY hh: mm:） >： 捕获到异常时收集 cpu 属性。  WMI 查询可能已失败。  警告。  
  
 为了解决此问题，请验证以下配置设置：  
  
-   在 Windows Server 2003 上的 SQL Server 代理服务必须是托管实例上的 Windows 性能监视组的一部分[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例上必须启用和配置 WMI 服务。  
  
-   WMI 存储库可能已损坏的托管实例上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   性能库可能已经丢失或损坏的托管实例上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
 为了确认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的指定实例已正确配置为向 UCP 报告数据，请验证在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的指定实例上以下类可用并且这些类对于 SQL Server 代理服务帐户而言是可访问的：  
  
-   Win32_MountPoint  
  
-   Win32_PerfRawData_PerfProc_Process  
  
-   Win32_PerfRawData_PerfOS_Processor  
  
-   Win32_Processor  
  
-   Win32_Volume  
  
-   Win32_LogicalDisk  
  
 您可以对上述每个类使用 Get-WmiObject PowerShell cmdlet 命令，以便验证每个类都是可访问的。 托管实例上运行以下 cmdlet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
```  
Get-WmiObject Win32_MountPoint -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_PerfRawData_PerfProc_Process -ErrorAction Stop| Out-Null  
Get-WmiObject Win32_PerfRawData_PerfOS_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Processor -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_Volume -ErrorAction Stop | Out-Null  
Get-WmiObject Win32_LogicalDisk -ErrorAction Stop | Out-Null  
```  
  
 有关 WMI 疑难解答的详细信息，请参阅[WMI 疑难解答](http://go.microsoft.com/fwlink/?LinkId=178250)。 请注意，这些 SQL Server 实用工具操作中的查询在本地运行，因此，DCOM 和远程故障排除内容不适用。  
  
## <a name="failed-data-collection"></a>失败的数据收集  
 如果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实用工具数据收集事件失败，请考虑以下可能性：  
  
-   不要更改 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的托管实例上“实用工具信息”收集组的任何属性，并且不要手动打开或关闭数据收集，因为数据收集由实用工具代理作业控制。  
  
-   失败的或不支持的 WMI 验证。 有关详细信息，请参阅本主题前面的“失败的 WMI 验证”部分。  
  
-   为中的数据刷新托管的实例列表视图中中的数据[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实用工具视点不会自动刷新。 要刷新数据，请右键单击**托管实例**中的节点**实用工具资源管理器导航**窗格中，然后选择**刷新**，或右键单击[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例名称在列表视图中，然后选择**刷新**。 请注意，在已向某一 UCP 注册 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的某一实例后，可能需要最长 30 分钟的时间，数据才会首次出现在实用工具资源管理器内容窗格的面板和视点中。  
  
-   使用 SQL Server 配置管理器来验证实例[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]正在运行。  
  
-   如果数据收集或数据上载由于超时问题而失败，则更新 MSDB 数据库中的函数 dbo.fn_sysutility_mi_get_collect_script()。 具体而言，在函数“Invoke-BulkCopyCommand()”中添加行：  
  
    ```  
    $bulkCopy.BulkCopyTimeout=180  
    ```  
  
     默认超时值为 30 秒。  
  
-   如果该 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例未群集化，则验证 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理服务是否正在运行并且该服务是否设置为在该 UCP 上以及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例上自动启动。  
  
-   验证使用了有效的帐户的托管实例上运行数据收集[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 例如，密码可能已到期。 如果代理密码已到期，则更新 SSMS 中的密码凭据，如下所示：  
  
    1.  在 SSMS 的 **“对象资源管理器”** 中，展开 **“安全性”** 节点，然后展开 **“凭据”** 节点。  
  
    2.  右键单击**UtilityAgentProxyCredential_\<GUID >** 和选择**属性**。  
  
    3.  在凭据属性对话框中，更新为所需的凭据**UtilityAgentProxyCredential_\<GUID >** 凭据。  
  
    4.  单击 **“确定”** 以确认更改。  
  
-   在 UCP 上和托管实例上，应启用 TCP/IP [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 启用通过 TCP/IP[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]配置管理器。  
  
-   UCP 上的 SQL Server Browser 服务必须启动，并且它必须配置为自动启动。 如果您的组织禁止使用 SQL Server Browser 服务，则使用以下步骤可以允许 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例连接到 UCP：  
  
    1.  在 Windows 任务栏上的托管实例上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，单击**启动**，然后单击**运行...**.  
  
    2.  在提供的空间中键入“cliconfg.exe”，然后单击 **“确定”**。  
  
    3.  如果提示允许“SQL 客户端配置实用工具 EXE”启动，则单击 **“继续”**。  
  
    4.  在 **“SQL Server 客户端网络实用工具”** 对话框上，选择 **“别名”** 选项卡，然后单击 **“添加…”**。  
  
    5.  在 **“添加网络库配置”** 对话框上：  
  
    6.  从网络库的列表中指定 TCP/IP。  
  
    7.  在 **“服务器别名”** 文本框中指定 UCP 的 ComputerName\InstanceName。  
  
    8.  在 **“服务器名称”** 文本框中指定 UCP 的 ComputerName。  
  
    9. 取消选中 **“动态确定端口”** 复选框。  
  
    10. 在 **“端口号”** 文本框中指定 UCP 正在侦听的端口号。  
  
    11. 单击 **“确定”** 保存所做的更改。  
  
    12. 对每个托管实例重复上述步骤[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用于将连接到 SQL Server Browser 服务未启用的其中一个 UCP。  
  
-   确保的托管实例[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]连接到网络。  
  
-   如果在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的托管实例上存在名称相同但区分大小写设置不同的数据库，则数据库及其视点之间的标识可能不正确，并且导致失败的数据收集。 例如，名为“MYDATABASE”的数据库可能显示名为“MyDatabase”的数据库的运行状态。 在此情况下不产生任何错误。 失败的数据收集可能还源自 UCP 中显示的其他对象（例如数据库文件和文件组名称）中的区分大小写设置不匹配。  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的某一托管实例承载在 Windows Server 2003 计算机上，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理服务帐户必须属于性能监视器用户安全组或本地管理员组。 否则，数据收集将失败并且具有拒绝访问错误。 若要添加[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到性能监视器用户安全组，代理服务帐户使用以下步骤：  
  
    1.  依次打开 **“计算机管理”**、 **“本地用户和组”**、 **“组”**。  
  
    2.  右键单击 **“性能监视器用户”** ，然后选择 **“添加到组”**。  
  
    3.  单击 **“添加”**。  
  
    4.  输入 SQL Server 代理服务正基于其运行的帐户，然后单击 **“确定”**。  
  
    5.  如果在将用户添加到该组之前，该 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例已向 UCP 注册，则重新启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理服务。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 实用工具的功能和任务](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [SQL Server 资源运行状况故障排除（SQL Server 实用工具）](../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)  
  
  