---
title: 升级 SQL Server 故障转移群集实例（安装程序）| Microsoft Docs
ms.custom: ''
ms.date: 01/22/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0e5232f1f8cad8ba9e6dc4ffcb9d838614a8c2c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044701"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>升级 SQL Server 故障转移群集实例（安装程序）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序 UI 或从命令提示符处将 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 故障转移群集升级为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集。  
  
 对于本地安装，必须以管理员身份运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取权限的域帐户。  
  
 升级前，请参阅 [升级 SQL Server 故障转移群集实例](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
##  <a name="UpgradeSteps"></a> 升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集  
  
#### <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集  
  
1.  在与你要升级的版本相匹配的版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装媒体中，双击根文件夹中的 setup.exe。 如果之前未安装必备组件，可能会要求您安装它们。  
  
2.  必备组件安装完成后，安装向导会启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装中心。 若要升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的现有实例，请选择你的实例。  
  
3.  如果需要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序支持文件， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序将安装它们。 如果安装程序指示您重新启动计算机，请在继续操作之前重新启动。  
  
4.  系统配置检查器将在您的计算机上运行发现操作。 若要继续， [!INCLUDE[clickOK](../../../includes/clickok-md.md)]。  
  
5.  在“产品密钥”页上输入与旧产品版本匹配的新版本的 PID 密钥。 例如，若要升级 Enterprise 故障转移群集，必须提供 [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]的 PID 密钥。 单击 **“下一步”** 继续。 请注意，对于同一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的所有故障转移群集节点，用于故障转移群集升级的 PID 密钥必须一致。  
  
6.  在“许可条款”页上阅读许可协议，然后选中相应的复选框以接受许可条款和条件。 为了帮助改进 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您还可以启用功能使用情况选项并将报告发送给 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]。 单击 **“下一步”** 继续。 若要结束安装程序，请单击 **“取消”**。  
  
7.  在“选择实例”页上指定要升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]实例。 单击 **“下一步”** 继续。  
  
8.  在“功能选择”页上会预先选择要升级的功能。 选择功能名称后，右侧窗格中会显示每个组件组的说明。 请注意，您不能更改要升级的功能，并且不能在升级操作过程中添加功能。 若要在升级操作完成后向 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 的已升级实例中添加功能，请参阅 [向 SQL Server 2016 的实例添加功能（安装程序）](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)。  
  
     在右侧窗格中显示所选功能的必备组件。 SQL Server 安装程序将在本过程后面所述的安装步骤中安装尚未安装的必备组件。 为了节省时间，应在每个节点上预安装这些必备组件。  
  
9. 在“实例配置”页上，那些字段自动从旧实例进行填充。 您可以选择指定新的 InstanceID 值。  
  
     **实例 ID** - 默认情况下，实例名称用作实例 ID。 这用于标识 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例的默认方式都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请选中 **“实例 ID”** 复选框，并提供一个值。 如果覆盖默认值，则必须为所有故障转移群集节点上要升级的实例指定相同的实例 ID。 已升级的实例的实例 ID 必须在所有节点上匹配。  
  
     **检测到的实例和功能** - 该网格显示运行安装程序的计算机上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。 单击 **“下一步”** 继续。  
  
10. “磁盘空间要求”页计算指定的功能所需的磁盘空间，并将磁盘空间要求与正在运行安装程序的计算机上的可用磁盘空间进行比较。  
  
11. 在“全文搜索升级”页上为所升级的数据库指定升级选项。 有关详细信息，请参阅 [全文搜索升级选项](https://msdn.microsoft.com/library/16c9376b-5fbb-4495-a429-06a2493849c9)。  
  
12. 在 **“错误报告”** 页上，指定要发送到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 以帮助改进 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的信息。 默认情况下，将启用用于错误报告的选项。  
  
13. 在升级操作开始之前，系统配置检查器将运行多组规则来针对您指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能验证您的计算机配置。  
  
14. “群集升级报告”页显示故障转移群集实例中的节点列表和每个节点上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 组件的实例版本信息。 它显示数据库脚本状态和复制脚本状态。 此外，还会显示有关单击 **“下一步”** 时会发生的情况的信息性消息。 根据已升级的故障转移群集节点数和节点总数，安装程序会显示你单击“下一步” 时发生的故障转移行为。 如果您尚未安装必备组件，还会就潜在的不必要停机时间向您发出警告。  
  
15. “准备升级”页显示您在安装过程中指定的安装选项的树视图。 若要继续，请单击 **“升级”**。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装程序将首先安装所选功能的必备组件，然后安装所选功能。  
  
16. 在升级过程中，“进度”页会提供相应的状态，因此您可以在安装程序进行的过程中监视当前节点上的升级进度。  
  
17. 完成当前节点的升级后，“群集升级报告”页将显示所有故障转移群集节点的升级状态信息、每个故障转移群集节点上的功能及其版本信息。 确认显示的版本信息正确，然后继续对剩余节点进行升级。 如果发生了向已升级的节点进行的故障转移，则也会显示在状态页上。 您还可以登入 Windows 群集管理员工具以进行确认。  
  
18. 升级完成后，“完成”页会提供指向安装摘要日志文件以及其他重要说明的链接。 若要完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安装过程，请单击 **“关闭”**。  
  
19. 如果安装程序指示您重新启动计算机，请立即重新启动。 安装完成后，请务必阅读来自安装向导的消息。 有关安装程序日志文件的详细信息，请参阅 [查看和阅读 SQL Server 安装程序日志文件](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
20. 若要完成升级过程，请在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集的所有其他节点上重复这些步骤。  
  
## <a name="to-upgrade-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集  
  
#### <a name="to-upgrade-to-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster-existing-includessnoversionincludesssnoversion-mdmd-cluster-is-a-non-multi-subnet-cluster"></a>升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集（现有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 群集是非多子网群集）。  
  
1.  按照上述步骤将群集升级到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
2.  使用 AddNode 安装程序操作添加不同子网上的节点，并确认在 **“群集网络配置”** 页将 IP 地址资源依赖关系更改为 OR。 有关详细信息，请参阅[在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>当前使用拉伸 V-LAN 升级多子网群集。  
  
1.  按照上述步骤将群集升级到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
2.  更改网络设置以将远程节点移到不同的子网。  
  
3.  使用 Windows 故障转移群集管理工具添加新子网的新 IP 地址，将 IP 地址资源依赖关系设置为 OR。  
  
## <a name="next-steps"></a>Next Steps  
 升级到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]后，请完成下列任务：  
  
-   [完成数据库引擎升级](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [更改数据库兼容性模式和使用 Query Store](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [利用新的 SQL Server 2016 功能](https://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)  
  
## <a name="see-also"></a>另请参阅  
 [升级 SQL Server 故障转移群集实例](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [查看和阅读 SQL Server 安装程序日志文件](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [向 SQL Server 2016 的实例添加功能（安装程序）](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  
