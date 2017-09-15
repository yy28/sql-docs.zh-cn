---
title: "使用安装向导安装 SQL Server 2016（安装程序）| Microsoft Docs"
ms.custom: 
ms.date: 09/06/2016
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
caps.latest.revision: 91
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: b97afc1f7fd9464e5ef5074e9e2b3d1ccb98d4b0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>使用安装向导安装 SQL Server（安装程序）

 > 本文介绍如何使用安装向导安装 SQL Server。 它适用于 [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] 和 [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)]。 有关与以前版本的 SQL Server 相关的内容，请参阅[使用安装向导安装 SQL Server 2014（安装程序）](http://msdn.microsoft.com/library/ms143219(SQL.120).aspx)。

本主题提供了使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的安装向导来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新实例的分步过程。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供了一个用于安装所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的功能树，这样您就不必分别安装这些组件了。 有关如何分别安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的详细信息，请参阅[安装 SQL Server](../../database-engine/install-windows/install-sql-server.md#how-to-install-individual-components)。  

 以下附加主题介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他安装方法：  

-   [从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
-   [使用配置文件安装 SQL Server](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
  
-   [使用 SysPrep 安装 SQL Server](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
  
-   [创建新的 SQL Server 故障转移群集（安装程序）](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   [使用安装向导升级 SQL Server（安装程序）](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) 

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>先决条件  
 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请查阅 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)中的主题。  
  
> [!NOTE]  
>  对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。  
 
 ###  <a name="bkmk_ga_instalpatch"></a> 安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  
  
## <a name="to-install-includessnoversionincludesssnoversion-mdmd"></a>安装 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质， 然后双击根文件夹中的 Setup.exe。 若要从网络共享进行安装，请找到共享中的根文件夹，然后双击 Setup.exe。  
  
1.  安装向导将运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心。 若要创建新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装，请单击左侧导航区域中的“安装”，然后单击“全新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 独立安装或向现有安装添加功能”。  

1.  在“产品密钥”页上，选择某个选项以指示您是安装免费版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，还是安装具有 PID 密钥的产品的生产版本。 有关详细信息，请参阅 [SQL Server 2017 的各版本和支持的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
     若要继续，请单击 **“下一步”**。  

1.  在“许可条款”页上查看许可协议，如果同意，请选中 **“我接受许可条款”** 复选框，然后单击 **“下一步”**。 为了帮助改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您还可以启用功能使用情况选项并将报告发送给 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
1.  在“全局规则”窗口中，如果没有规则错误，安装过程将自动前进到“产品更新”窗口。  
  
1.  如果未在“控制面板”\“所有控制面板项”\“Windows 更新”\“更改设置”中选中“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”复选框，则接下来将显示“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”页。 在“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”页中选中选项会将计算机设置更改为在您浏览 Windows 更新时包括最新更新。  

1.  在“产品更新”页中，将显示最近提供的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品更新。 如果未发现任何产品更新， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将不会显示该页并且自动前进到 **“安装安装程序文件”** 页。  

1.  在“安装安装程序文件”页上，安装程序将提供下载、提取和安装这些安装程序文件的进度。 如果找到了针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的更新，并且指定了包括该更新，则也将安装该更新。 如果未找到任何更新，安装程序将自动进行。 
  
1. 在安装规则上，SQL Server安装程序将进行检查以确定运行安装程序时可能出现的潜在问题。 如果出现故障，请单击“状态”列了解详细信息。 否则，单击“下一步”。 

1. 在“安装类型”上，选择执行新安装，或向现有安装添加功能。 单击 **“下一步”**。 
  
1. 在“功能选择”页上，选择要安装的组件。 例如，若要安装 SQL Server 数据库引擎的新实例，请选中“数据库引擎服务”。

    选择功能名称后， **“功能说明”** 窗格中会显示每个组件组的说明。 您可以选中任意一些复选框。 有关详细信息，请参阅 [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)和 [SQL Server 2016 的各个版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。
  
     **“所选功能的必备组件”** 窗格中将显示所选功能的必备组件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将在本过程后面所述的安装步骤中安装尚未安装的必备组件。  
  
     您还可以使用“功能选择”页底部的字段为共享组件指定自定义目录。 若要更改共享组件的安装路径，请更新该对话框底部字段中的路径，或单击 **“浏览”** 移动到另一个安装目录。 默认安装路径为 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]。  
  
     为共享组件指定的路径必须是绝对路径。 文件夹不能压缩或加密。 不支持映射的驱动器。  
  
     SQL Server 对共享功能使用两个目录：
  
     * 共享功能目录  
  
     * 共享功能目录 (x86)  
  
     为以上每个选项指定的路径必须不同。  
  
11. 如果所有规则均通过验证，则“功能规则”窗口将自动前进。  
  
12. 在“实例配置”页上指定是安装默认实例还是命名实例。 有关详细信息，请参阅 [Instance Configuration](../../sql-server/install/instance-configuration.md#instance-configuration)。  
  
     **实例 ID** - 默认情况下，实例名称用作实例 ID。 这用于标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例的默认方式都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请为“实例 ID”  文本框指定一个不同值。  
  
    > [!NOTE]  
    >  典型的 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]独立实例（无论是默认实例还是命名实例）不会对“实例 ID” 使用非默认值。  
  
     所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升级都将应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的每个组件。  
  
     **已安装的实例** — 该网格显示安装程序正在其中运行的计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 如果计算机上已经安装了一个默认实例，则必须安装 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]的命名实例。  
  
     安装程序中的其余工作流取决于您指定要安装的功能。 您可能不会看到所有的页面，具体取决于您进行的选择。  
  
13. 使用“服务器配置 — [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户”页指定服务的登录帐户。 此页上配置的实际服务取决于您选择安装的功能。  
  
     您可以为所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务分配相同的登录帐户，也可以单独配置各个服务帐户。 您还可以指定是自动启动、手动启动还是禁用服务。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您逐个配置服务帐户，以便为每项服务提供最低权限，其中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务将被授予完成其任务所必须具备的最低权限。 有关详细信息，请参阅 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
     若要为此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中的所有服务帐户指定同一个登录帐户，请在该页底部的字段中提供凭据。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     使用“服务器配置 — 排序规则”页为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定非默认排序规则。 有关详细信息，请参阅[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
14. 使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - 服务器配置”页指定以下各项：  
  
    -   安全模式 - 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例选择 Windows 身份验证或混合模式身份验证。 如果选择“混合模式身份验证”，则必须为内置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员帐户提供一个强密码。  
  
         在设备与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成功建立连接之后，用于 Windows 身份验证和混合模式身份验证的安全机制是相同的。 有关详细信息，请参阅 [数据库引擎配置 - 服务器配置](../../sql-server/install/instance-configuration.md#database-engine-configuration---server-configuration)。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员 - 您必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例至少指定一个系统管理员。 若要添加用以运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的帐户，请单击 **“添加当前用户”**。 若要向系统管理员列表中添加帐户或从中删除帐户，请单击 **“添加”** 或 **“删除”**，然后编辑将拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的管理员特权的用户、组或计算机的列表。  
  
     使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - 数据目录”页指定非默认的安装目录。 若要安装到默认目录，请单击 **“下一步”**。  
  
    > [!IMPORTANT]  
    >  如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。  
  
     有关详细信息，请参阅 [数据库引擎配置 - 数据目录](../../sql-server/install/instance-configuration.md#database-engine-configuration---data-directories)。  
  
     使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - FILESTREAM”页对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例启用 FILESTREAM。 有关详细信息，请参阅 [数据库引擎配置 - 文件流](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream)。  
  
     使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - TempDB”页，可以配置 TempDB 的文件大小、文件数、非默认的安装目录和文件增长设置。 有关详细信息，请参阅 [数据库引擎配置 - TempDB](../../sql-server/install/instance-configuration.md#database-engine-configuration---tempdb)。  
  
15. 使用“ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置 – 帐户设置”页指定服务器模式以及将拥有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]管理员权限的用户或帐户。 服务器模式决定哪些内存和存储子系统用于服务器。 不同的解决方案类型在不同的服务器模式下运行。 如果您计划在服务器上运行多维数据集数据库，则选择默认选项“多维”和“数据挖掘”服务器模式。 对于管理员权限，您必须为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定至少一个系统管理员。 若要添加当前正在运行 SQL Server 安装程序的帐户，请单击 **“添加当前用户”**按钮。 若要向系统管理员列表中添加帐户或从中删除帐户，请单击 **“添加”** 或 **“删除”**，然后编辑将拥有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的管理员特权的用户、组或计算机的列表。 有关服务器模式和管理员权限的详细信息，请参阅 [Analysis Services 配置-帐户设置](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning)。  

   完成对该列表的编辑后，请单击 **“确定”**。 验证配置对话框中的管理员列表。 完成此列表后，请单击 **“下一步”**。
   
   使用“ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置 - 数据目录”页指定非默认的安装目录。 若要安装到默认目录，请单击 **“下一步”**。  
   
   >[!IMPORTANT]  
   >在安装时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，如果为 INSTANCEDIR 和 SQLUSERDBDIR 指定相同的目录路径，SQL Server 代理和全文搜索则会由于缺少权限而无法启动。  
   >  
   >如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。  
   
   有关详细信息，请参阅 [Analysis Services 配置 - 数据目录](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories)。  
   
17. 使用“Distributed Replay 控制器配置”页可以指定您希望向其授予针对 Distributed Replay 控制器服务的管理权限的用户。 具有管理权限的用户将可以不受限制地访问 Distributed Replay 控制器服务。  
  
     单击 **“添加当前用户”** 按钮可以添加要向其授予针对 Distributed Replay 控制器服务的访问权限的用户。 单击 **“添加”** 按钮可以添加针对 Distributed Replay 控制器服务的访问权限。 单击 **“删除”** 按钮可以从 Distributed Replay 控制器服务中删除访问权限。  
  
     若要继续，请单击 **“下一步”**。  
  
18. 使用“ Distributed Replay 客户端配置”页可以指定您希望向其授予针对 Distributed Replay 客户端服务的管理权限的用户。 具有管理权限的用户将可以不受限制地访问 Distributed Replay 客户端服务。  
  
     “控制器名称”是一个可选参数，其默认值为 \<blank>。 输入客户端计算机将与 Distributed Replay 客户端服务进行通信的控制器的名称。 请注意以下事项：  
  
    -   如果您已经设置了一个控制器，则在配置每个客户端时输入该控制器的名称。  
  
    -   如果您尚未设置控制器，则可以将控制器名称保留为空白。 但是，您必须在 **“客户端配置”** 文件中手动输入控制器名称。  
  
     为 Distributed Replay 客户端服务指定 **“工作目录”** 。 默认工作目录为 \<驱动器号>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\。  
  
     为 Distributed Replay 客户端服务指定 **“结果目录”** 。 默认结果目录为 \<驱动器号>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\。  
  
     若要继续，请单击 **“下一步”**。  
  
19. “准备安装”页将显示安装期间指定的安装选项的树状视图。 在此页上，安装程序指示是启用还是禁用产品更新功能以及最终的更新版本。  
  
     若要继续，请单击 **“安装”**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将首先安装所选功能的必备组件，然后安装所选功能。  
  
20. 在安装过程中，“安装进度”页会提供相应的状态，因此您可以在安装过程中监视安装进度。  
  
21. 安装完成后，“完成”页会提供指向安装摘要日志文件以及其他重要说明的链接。 若要完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程，请单击 **“关闭”**。  
  
22. 如果安装程序指示您重新启动计算机，请立即重新启动。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="next-steps"></a>后续步骤  
 配置新安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 为了减少系统的可攻击外围应用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有选择地安装和启用了一些关键服务和功能。 有关详细信息，请参阅 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [验证 SQL Server 安装](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [修复失败的 SQL Server 2016 安装](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)   
 [查看和阅读 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [使用安装向导（安装程序）升级到 SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  

