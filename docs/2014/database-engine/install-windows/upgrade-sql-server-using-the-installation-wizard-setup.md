---
title: 使用安装向导（安装程序）升级到 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775387"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>使用安装向导升级到 SQL Server 2014（安装程序）
   安装向导提供了一个用来升级  组件的功能树。 也可以将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 与早期版本并行安装，或从早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迁移已有的数据库和配置设置，然后将它们应用于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的实例。  
  
 有关详细信息，请参阅以下主题：  
  
-   [支持的版本和版本升级](supported-version-and-edition-upgrades.md)  
  
-   [使用 SQL Server 的多个版本和实例](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [升级 SQL Server 故障转移群集实例（安装程序）](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [Install SQL Server 2014 from the Command Prompt](install-sql-server-from-the-command-prompt.md)  
  
-   [使用复制数据库向导](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Core SP1 的计算机上，不支持将早期版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升级到 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]。 有关服务器核心安装的详细信息，请参阅[在 Server core 上安装 SQL Server 2014](install-sql-server-on-server-core.md)。  
  
## <a name="prerequisites"></a>先决条件  
 您必须以管理员身份运行安装程序。 如果从远程共享位置安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，必须使用对该远程共享位置具有读取和执行权限的域帐户且是本地管理员。  
  
 升级[!INCLUDE[ssDE](../../includes/ssde-md.md)]之前，请先查看以下主题：  
  
-   [升级到 SQL Server 2014](upgrade-sql-server.md)  
  
-   [安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [系统配置检查器的检查参数](check-parameters-for-the-system-configuration-checker.md)  
  
-   [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server 数据库引擎的向后兼容性](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  请注意，您不能更改要升级的功能，并且不能在升级操作过程中添加功能。 有关如何在升级操作完成后向的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]已升级实例添加功能的详细信息，请参阅[将功能添加到 SQL Server 2014 &#40;安装&#41;的实例](add-features-to-an-instance-of-sql-server-setup.md)。  
  
## <a name="procedure"></a>过程  
  
#### <a name="to-upgrade-to-sscurrent"></a>升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质，然后双击根文件夹中的 Setup.exe。 若要从网络共享进行安装，请移动到共享中的根文件夹，然后双击 Setup.exe。  
  
2.  安装向导启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心。 若[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要升级的现有实例，请在左侧导航区域中单击 "**安装**"，然后单击 **"从[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或升级" **。  
  
3.  在“产品密钥”页上单击相应的选项，以指示您是升级到免费版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，还是您拥有该产品生产版本的 PID 密钥。 有关详细信息，请参阅[SQL Server 2014 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[支持的版本和版本升级](supported-version-and-edition-upgrades.md)。  
  
4.  在“许可条款”页上查看许可协议，如果同意，请选中 **“我接受许可条款”** 复选框，然后单击 **“下一步”**。 为了帮助改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您还可以启用功能使用情况选项并将报告发送给 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
5.  在“全局规则”窗口中，如果没有规则错误，安装过程将自动前进到“产品更新”窗口。  
  
6.  如果未在“控制面板”\“所有控制面板项”\“Windows 更新”\“更改设置”中选中“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”复选框，则接下来将显示“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”页。 在“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”页中选中选项会将计算机设置更改为在您浏览 Windows 更新时包括最新更新。  
  
7.  在“产品更新”页中，将显示最近提供的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品更新。 如果你不想包括更新，则取消选中“包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品更新”**** 复选框。 如果未发现任何产品更新， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将不会显示该页并且自动前进到 **“安装安装程序文件”** 页。  
  
8.  在“安装安装程序文件”页上，安装程序将提供下载、提取和安装这些安装程序文件的进度。 如果找到了针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的更新，并且指定了包括该更新，则也将安装该更新。  
  
9. 在“升级规则”窗口中，如果没有规则错误，安装过程将自动前进到“选择实例”窗口。  
  
10. 在“选择实例”页上指定要升级的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 若要升级管理工具和共享功能，请选择 **“仅升级共享功能”**。  
  
11. 在“选择功能”页上会预先选择要升级的功能。 选择功能名称后，右侧窗格中会显示每个组件组的说明。  
  
     在右侧窗格中显示所选功能的必备组件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将在本过程后面所述的安装步骤中安装尚未安装的必备组件。  
  
    > [!NOTE]  
    >  如果你已选择通过选择 "**选择实例**" 页上的 " ** \<仅升级共享功能">** 来升级共享功能，则在 "功能选择" 页上预先选择了所有共享功能。 所有共享组件将同时升级。  
  
12. 在“实例配置”页上，指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的实例 ID。  
  
     **实例 id** -默认情况下，实例名称用作实例 id。 这用于标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请为“实例 ID”**** 文本框提供一个值。  
  
     所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升级都将应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的每个组件。  
  
     **已安装的实例** - 该网格显示安装程序正在其中运行的计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 如果计算机上已经安装了一个默认实例，则必须安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的命名实例。  
  
13. 本主题中的其余工作流取决于要安装的功能。 您可能不会看到所有的页面，具体取决于您进行的选择。  
  
14. 在“服务器配置 - 服务帐户”页上，显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的默认服务帐户。 此页上配置的实际服务取决于要升级的功能。  
  
     身份验证和登录信息将从早期的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例继承。 您可以为所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务分配相同的登录帐户，也可以单独配置各个服务帐户。 您还可以指定是自动启动、手动启动还是禁用服务。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议对各服务帐户进行单独配置，以便向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务授予它们完成各自任务所必须拥有的最低权限。 有关详细信息，请参阅[配置 Windows 服务帐户和权限](../configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
     若要为此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中的所有服务帐户指定相同的登录帐户，请在页面底部的字段中提供凭据。  
  
     **安全说明** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务指定登录信息后，请单击 **“下一步”**。  
  
15. 在“全文搜索升级选项”页上为所升级的数据库指定升级选项。 有关详细信息，请参阅 [全文搜索升级选项](../../sql-server/install/full-text-search-upgrade-options.md)。  
  
16. 如果所有规则均通过验证，则“功能规则”窗口将自动前进。  
  
17. “准备升级”页显示您在安装过程中指定的安装选项的树视图。 若要继续，请单击 **“安装”**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将首先安装所选功能的必备组件，然后安装所选功能。  
  
18. 在安装过程中，进度页会提供相应的状态，因此您可以在安装过程中监视安装进度。  
  
19. 安装完成后，“完成”页会提供指向安装摘要日志文件以及其他重要说明的链接。 若要完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程，请单击 **“关闭”**。  
  
20. 如果安装程序指示您重新启动计算机，请立即重新启动。 安装完成后，请务必阅读来自安装向导的消息。 有关安装程序日志文件的详细信息，请参阅 [查看和阅读 SQL Server 安装程序日志文件](view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="next-steps"></a>后续步骤  
 升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后，请完成下列任务：  
  
-   **注册服务器** - 升级会删除早期的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的注册表设置。 升级之后，必须重新注册服务器。  
  
-   **更新统计信息** - 为了帮助优化查询性能，建议在升级之后更新所有数据库的统计信息。 使用 `sp_updatestats` 存储过程可以更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中用户定义的表中的统计信息。  
  
-   **配置新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装**-为了减少系统的外围应用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以有选择地安装和启用密钥服务和功能。 有关外围应用配置器工具的详细信息，请参阅此版本的自述文件。  
  
## <a name="see-also"></a>另请参阅  
 [升级到 SQL Server 2014](upgrade-sql-server.md)   
 [向后兼容性](../../getting-started/backward-compatibility.md)  
  
  
