---
title: Master Data Services 的高可用性和灾难恢复 | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2017
ms.prod: sql
ms.prod_service: mds
ms.component: installing-mds-in-an-alwayson-group-environment
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7e3bd1f050b1f5652a12e74066345e8d20e8286f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Master Data Services 的高可用性和灾难恢复

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]


**摘要：** 本文介绍了一种解决方案，该解决方案适用于 AlwaysOn 可用性组配置上托管的 Master Data Service (MDS)。 本文介绍了如何在 SQL 2016 AlwaysOn 可用性组 (AG) 上安装和配置 SQL 2016 Master Data Services。 此解决方案的主要目的是改善 SQL Server 数据库上托管的 MDS 后端数据的高可用性和灾难恢复。

## <a name="introduction"></a>简介


本文介绍了一种解决方案，该解决方案适用于 AlwaysOn 可用性组配置上托管的 Master Data Service (MDS)。 本文介绍了如何在 SQL 2016 AlwaysOn 可用性组 (AG) 上安装和配置 SQL 2016 MDS。 此解决方案的主要目的是改善 SQL Server 数据库上托管的 MDS 后端数据的高可用性和灾难恢复。

若要实现该解决方案，需完成本文所述的以下任务。

1.  [安装并设置 Windows Server 故障转移群集 (WSFC)](#windows-server-failover-cluster-wsfc)。

2.  [设置 AlwaysOn AG](#sql-server-alwayson-availability-group)。

3.  [将 MDS 配置为在 WSFC 节点上运行](#configure-mds-to-run-on-an-wsfc-node)。

以上部分在简要介绍这些技术后，再进行详细说明。 有关这些技术的详细信息，请查看每个部分中链接的文档。

本文所述的此解决方案基于 SQL Server AlwaysOn AG，其中每个数据库都具有多个同步或异步副本。 只有一个副本接收事务（接收用户请求）。 这就是主要副本。

每个副本都有自己的存储器，因此本解决方案中没有集中的共享存储。 当存在软件故障或硬件故障影响主要副本时，可根据配置和情况自动或手动将主要副本故障转移到同步或异步复制。 这样通过最大程度地降低用户受到的中断影响，保证了数据库的高可用性。

异步副本通常托管在远离主要副本数据中心的数据中心上。 在发生灾难的情况下，可将主要副本故障转移到另一个数据中心。 这样保证了数据库的灾难恢复。

出于演示目的，本文所述的解决方案使用以下版本的软件。 旧版的操作相同，但可能会存在细微差别。

-   带 Server 故障转移群集的 Windows Server 2012R2

-   带 Master Data Service 功能的 SQL Server 2016

此外，该解决方案使用两个 VM（MDS-HA1 和 MDS-HA2）来托管两个副本。 只要 SQL Server AlwaysOn AG 支持，MDS 就不会限制使用的副本数量。

本文假定你已具备 Windows Server、Windows Server 故障转移群集、SQL Server AlwaysOn 和 SQL Server MDS 的基本知识。

## <a name="what-is-not-covered"></a>不包含的内容

本文档不包含以下内容：

-   如何实现 IIS（托管 Master Data Service UI 的 Web 服务器）的高可用性和在灾难后进行恢复。 MDS 不会对 IIS 施加任何特定要求，因此实现 IIS 高可用性和负载均衡的标准技术也适用于此处。

-   如何使用 SQL Server AlwaysOn 故障转移 (FCI) 群集支持 MDS 后端的高可用性 (HA)。 SQL Server 故障转移群集是另外一种 HA 解决方案，受到 SQL Server 的正式支持，并且适用于 MDS。

-   如何使用 SQL Server 故障转移群集 (FCI) 的混合解决方案和 AlwaysOn AG 来支持 MDS 后端的高可用性 (HA)。 该混合解决方案适用于 MDS。

## <a name="design-consideration"></a>设计注意事项

图 1 所示为常用于 AlwaysOn AG 的典型配置。 在主数据中心，存在两个具有同步提交关系的副本，且两个副本都具备投票特权。 通常会用其改进 HA，以防主要副本出现故障。

在灾难恢复数据中心，存在一个与主要副本有异步提交关系的次要副本。 此数据中心通常位于不同于主要数据中心的地理区域。 次要副本不具备投票特权。

万一主要数据中心发生火灾、地震等灾难，则使用此配置实现恢复。此配置可以较低成本实现 HA 和灾难恢复。

![用于 AlwaysOn 可用性组的典型解决方案](media/Fig1_TypicalConfig.png)

图 1. 一种典型的 AlwaysOn 可用性组配置

如果不需要考虑灾难恢复，在第二个数据中心则无需副本。 如果需改进 HA，可在同一主要数据中心拥有更多同步副本。

因此务必考虑你的情况和要求，然后再选择所需异步和同步副本的数量以及需要放入这些副本的数据中心。

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server 故障转移群集 (WSFC)

本部分包含以下任务。

1.  [安装 Windows 故障转移群集功能](#install-failover-cluster-feature)。

2.  [创建 Windows Server 故障转移群集](#create-a-windows-server-failover-cluster)。

如前一部分中的图 1 所示，本文所述的解决方案包括 Windows Server 故障转移群集 (WSFC)。 由于 SQL AlwaysOn 进行故障检测和故障转移时依赖于 WFSC，因此需要安装 WSFC。

WSFC 是一种用于提升应用程序服务高可用性的功能。 它由一组独立的 Windows Server 实例以及在这些实例上运行的 Microsoft 故障转移群集服务组成。 这些 Windows Server 实例（或有时被称为节点）彼此连接，以实现相互通信，这样就可以进行故障检测。 WSFC 提供故障检测和故障转移功能。 如果群集中的某个节点或服务出现故障，则会检测到该故障，并且另一个节点将自动或手动开始提供托管在故障节点上的服务。 因此，用户仅遇到最小程度的服务中断，服务可用性得以提升。  

### <a name="prerequisites"></a>必备条件

所有实例都已安装 Windows Server 操作系统，并且所有更新都已修补。

>[!NOTE] 
>强烈建议在所有实例上安装相同的 Windows 版本和功能集，以避免出现任何潜在的不兼容问题。

### <a name="install-failover-cluster-feature"></a>安装故障转移群集功能

对每个 Windows Server 实例完成以下步骤，在每个实例上安装 WSFC 功能。 你需要管理员权限。

1.  打开 Windows Server 中的“服务器管理器”，然后在右窗格中单击“添加角色和功能”。 此操作会启动“添加角色和功能向导”。

2.  单击“下一步”直到出现“功能”页。

3.  选择“故障转移群集”复选框，然后单击“下一步”完成安装。 请参阅图 2。

    如果要求确认“添加故障转移群集的所需功能”，请单击“添加功能”。 请参阅图 3。

    ![添加角色和功能向导、故障转移群集](media/Fig2_SelectFeatures.png)

    图 2

    ![添加故障转移群集所需的角色和功能向导](media/Fig3_RequiredFeaturesFailover.png)

    图 3

4.  在“确认”页上，单击“安装”，安装故障转移群集功能。

5.  在“结果”页上，确保所有内容均安装成功，且没有出现错误和警告。

### <a name="create-a-windows-server-failover-cluster"></a>创建 Windows Server 故障转移群集

在所有实例上安装 WSFC 功能之后，即可配置 WSFC。 只需在一个节点上执行此操作。

1.  打开 Windows Server 中的服务器管理器，然后单击右上角“工具”菜单上的故障转移群集管理器以启动管理器。

2.  在故障转移群集管理器的右窗格中，单击“验证配置”。 请参阅图 4。

    ![故障转移群集管理器、验证配置](media/Fig4_ValidateConfig.png)

    图 4

3.  在“验证配置向导”中，单击“下一步”。

4.  在“选择服务器或群集”对话框中，添加将要托管 SQL Server 的服务器名称，然后单击“下一步”。 请参阅图 5。

    在此示例中添加了两个实例：MDS-HA1 和 MDS-HA2。

    ![验证配置向导、选择服务器或群集页](media/Fig5_AddServer.png)

    图 5

5.  在“测试选项”页上，单击“运行所有测试”，然后单击“下一步”。

6.  单击“下一步”完成验证。

    “验证”页显示进度，“摘要”页显示验证摘要。 请参阅图 6 和图 7。

7.  在“摘要”页上，检查是否出现任何警告或错误消息。

    请务必修复错误。 但警告可能不表示项目存在问题。 警告消息是指“测试的项目虽符合要求，但有一些需要进行检查”。 例如，图 7 所示为一条“验证磁盘访问延迟”警告，这可能是由于磁盘暂时忙于其他任务，可以忽略此警告。 应当查看每个警告和错误消息的在线文档以获取更多详细信息。 请参阅图 7。
 
    ![验证配置向导、验证页](media/Fig6_ValidationTests.png)

    图 6

    ![验证配置向导、摘要页](media/Fig7_ValidationSummary.png)

    图 7

8.  在“摘要”页上，确认选中“立即使用验证节点创建群集”复选框，然后单击“完成”以启动“创建群集向导”。

9.  在“创建群集向导”中，单击“下一步”。

10. 在“管理群集的访问点”页上，输入 WSFC 群集名称，然后单击“下一步”。 在此示例中，使用“MDS-HA”作为群集名称。 请参阅图 8。

    ![输入群集名称](media/Fig8_EnterClusterName.png)

    图 8

11. 继续单击“下一步”以完成群集的创建。 “群集 MDS-HA 的摘要”部分显示群集信息。 请参阅图 9。

    ![查看群集的摘要信息](media/Fig9_ClusterSummary.png)

    图 9

    稍后如需添加节点，请在故障转移群集管理器的右窗格中单击“添加节点”操作。

注意：

-   不是所有版本的 Windows Server 都具备 WSFC 功能。 请确保你的版本具备该功能。

-   请确保你拥有适当特权在 Active Directory 中安装 WSFC。 如有任何问题，请参阅 [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx)（故障转移群集分步指南：在 Active Directory 中配置帐户）。

有关 WSFC 的更多详细信息，请参阅[故障转移群集](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx)。

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 可用性组

本部分包含以下任务。

1.  [启用 SQL Server AlwaysOn 可用性组](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)。

2.  [创建可用性组](#create-an-availability-group)。

3.  [验证并测试可用性组](#validation-and-test-the-availability-group)。

SQLServer AlwaysOn 解决方案为 SQLServer 数据库提供高可用性和灾难恢复。 AlwaysOn 有两种可能的解决方案。
两种解决方案都基于 WSFC。

-   AlwaysOn 可用性组 (AG)

-   AlwaysOn 故障转移群集实例 (FCI)。

AG 可增强数据库级别的高可用性。 AG（一组用户数据库）及其虚拟网络名称均在 WSFC 中注册为资源。

FCI 可增强实例级别的高可用性。 SQL Server 服务及相关服务均在 WSFC 中注册为资源。 此外，FCI 解决方案需要对称的共享磁盘存储（例如 SAN 或 SMB 文件共享），这些存储必须适用于 WFC 群集中的所有节点。


### <a name="prerequisites"></a>必备条件

-   在所有节点上安装 SQL Server。 有关详细信息，请参阅[安装 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server)。

-   （推荐）在每个节点上安装完全相同的 SQL Server 功能集和版本。 特别是必须安装 MDS。

-   （推荐）对每个 SQL Server 实例使用相同的配置。 特别是必须对所有 SQL Server 实例配置相同的服务器排序规则。

-   （推荐）使用相同的服务帐户运行每个 SQL Server 实例。 否则，必须对每个 SQL Server 实例授予权限，以确保 SQL Server 实例能够相互通信。

-   请确认 Windows 防火墙设置允许 SQL Server 实例相互通信。

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>在每个 SQL Server 实例上启用 SQL Server AlwaysOn 可用性组

1.  在 SQL Server 配置管理器中，在左窗格中单击“SQL Server 服务”，在右窗格中右键单击“SQL Server”，然后单击“属性”。 请参阅图 10。

    ![SQL Server 属性窗口](media/Fig10_SQLServerProperties.png)

    图 10

2.  在“SQL Server (MSSQLSERVER) 属性”对话框中，单击“AlwaysOn 高可用性”选项卡，然后选中“启用 AlwaysOn 可用性组”复选框。 当“Windows 故障转移群集名称”文本框中显示值时，单击“确定”继续。 请参阅图 11。

    ![启用“AlwaysOn 可用性组”选项](media/Fig11_EnableAlwaysOn.png)

    图 11

3.  当显示警告页时，单击“确定”继续。 请参阅图 12。

    ![确认以停止并重新启动服务](media/Fig12_WarningServiceStopStart.png)

    图 12

4.  单击“重新启动”，重新启动“SQL Server”服务并让此更改生效。 请参阅图 10。

>[!NOTE] 
>可使用 SQL Server 配置管理器更改运行 SQL Server 服务的服务帐户。 在“SQL Server (MSSQLSERVER) 属性”对话框中，单击“登录”选项卡。 请参阅图 11。

### <a name="create-an-availability-group"></a>创建可用性组

在所有 SQL Server 实例中启用 AlwaysOn 功能后，即可在节点上创建一个包含 MDS 数据库的新建 AG。

AG 只能在现有数据库上创建。 因此，可在一个节点上创建 MDS 数据库，或创建临时数据库，然后再删除此临时数据库。 在此示例中，我们将创建一个 emptyMDS 数据库并在此 MDS 数据库上创建一个 AG。

1.  在节点上启动 SQL Server Management Studio (SSMS)，并使用相应凭据连接到本地 SQL Server 实例。

2.  在 SSMS 中，打开一个“新建查询”窗口，运行以下脚本以创建空数据库。 将 C:\\temp 替换为要用于执行完整备份的位置。

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >在此数据库上创建 AG 时需要完整的数据库备份。

3.  在对象资源管理器中，展开“AlwaysOn 高可用性”文件夹，然后单击“新建可用性组向导”以启动“新建可用性组向导”。 请参阅图 13。

    ![启动新建可用性组向导](media/Fig13_AvailabilityGroupsFolder.png)

    图 13

4.  在“新建可用性组”向导中，单击“下一步”以显示“指定名称”页。 键入 AG 的名称，然后单击“下一步”。 请参阅图 14。

    ![输入可用性组的名称](media/Fig14_AvailabilityGroupName.png)

    图 14

5.  单击刚在“选择数据库”页上创建的数据库，然后单击“下一步”。 请参阅图 15。

    ![选择数据库](media/Fig15_AvailabilityGroupSelectDatabase.png)

    图 15

6.  在“指定副本”页上，单击“添加副本”以添加其他副本。 此页已将当前的本地 SQL Server 实例列为副本。 请参阅图 16。

7.  在“连接到服务器”对话框中，添加相应凭据并单击“连接”。

    ![连接到 SQL Server 实例](media/Fig16_AddReplicaConnectServer.png)

    图 16

    现在可在列表中看到两个副本。 重复此步骤，将其他节点添加为副本。 请参阅图 17。

    ![查看副本列表](media/Fig17_AvailabilityGroupSQLReplicas.png)

    图 17

    对每个副本配置以下“同步提交”、“自动故障转移”和“可读辅助副本”设置。 请参阅图
17.

    同步提交：确保在数据库的主要副本上提交事务时，在所有其他同步副本上也提交了该事务。 异步提交则不能保证这一点，并且会落后于主要副本。

    通常只有当两个节点位于同一数据中心时，才能启用同步提交。 如果它们处于不同的数据中心，同步提交会降低数据库的性能。

    如果未选中此复选框，则使用异步提交。

    自动故障转移：关闭主要副本，选择自动故障转移时，AG 会自动故障转移到其次要副本。 只有在使用同步提交的副本上才能够启用。

    可读辅助副本：默认情况下，用户无法连接到任何次要副本。 用户只能连接到使用只读访问的次要副本。

8.  在“指定副本”页上，单击“侦听器”选项卡，执行以下操作。 请参阅图 18。

    A.  单击“创建可用性组侦听器”以设置 MDS 数据库连接的可用性组侦听器。

    B.  输入“侦听器 DNS 名称”，例如 MDSSQLServer。

    c.  在“端口”文本框中输入默认 SQL 端口 (1433)。

    d.  在“网络模式”文本框中输入 DHCP，然后单击“下一步”继续。

    >[!NOTE] 
    >或者，可以选择“静态 IP”作为“网络模式”并输入静态 IP。 也可输入不同于 1433 的端口。 

    ![配置侦听器](media/Fig18_AvailabilityGroupCreateListener.png)

    图 18

9.  在“选择数据同步”页上，单击“完整”，然后指定每个节点都能访问的网络共享。 单击 **“下一步”** 继续。 请参阅图 19。

    此网络共享用于存储数据库备份以创建次要副本。 如果它不适用于你的组织，请选择其他数据同步选项。 请参考 [SQL Server 2016 AlwaysOn 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)，了解如何使用其他选项创建次要副本。 图 17 还列出了其他选项。

    ![配置数据同步](media/Fig19_AvailabilityGroupDataSync.png)

    图 19 

10. 在“验证”页上，确保所有验证均传递成功，并更正所有错误。 单击 **“下一步”** 继续。

11. 在“摘要”页上查看所有配置设置，然后单击“完成”。 此操作将创建并配置可用性组。

12. 在“结果”页上，确认所有必要步骤均已完成。

### <a name="validation-and-test-the-availability-group"></a>验证并测试可用性组

1.  打开 SSMS，连接到在[创建可用性](#create-an-availability-group)部分所创建的侦听器 DNS 名称。 在此示例中，为 MDSSQLServer。

2.  在对象资源管理器中，展开“AlwaysOn 高可用性”文件夹，右键单击在[创建可用性组](#create-an-availability-group)部分所创建的 AG，然后单击“显示仪表板”。 请参阅图 20。 将会出现新建 AG 及其副本的状态。

    ![查看仪表板](media/Fig20_ShowDashboard.png)

    图 20 

3.  单击“故障转移”，对同步副本和异步副本执行故障转移。 此操作是为了验证故障转移是否正确运行，未出现任何问题。

 AlwaysOn 的安装已完成。

有关 AlwaysOn 可用性组的详细信息，请参阅 [SQL Server 2016 AlwaysOn 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)。

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>将 MDS 配置为在 WSFC 节点上运行

本文介绍的此解决方案仅需在 WSFC 上运行的 MDS 后端数据库。 只要 MDS 能够连接到 AG，MDS 的其他部分（如 Web 应用程序和 MDS 配置管理器）就可在 WSFC 内外的节点上运行。

1.  在一个节点上打开 Master Data Service 配置管理器，依次单击“数据库配置”和“创建数据库”，启动“创建数据库向导”。

2.  在“数据库服务器”页上的“SQL Server 实例”文本框中键入 AG 侦听器的 DNS 名称，单击“测试连接”，然后单击“下一步”。 请参阅图 21。

    ![使用 AG 侦听器配置数据库服务器](media/Fig21_MDSDatabaseServerListener.png)

    图 21

3.  在“数据库”页中，键入在[创建可用性组](#create-an-availability-group)部分所创建的数据库名称，然后单击“下一步”。 请参阅图 22。

    ![创建并配置数据库](media/Fig22_MDSCreateDatabase.png)

    图 22

4.  完成“创建数据库向导”。 有关详细信息，请参阅 [Master Data Services 的安装和配置](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

5.  单击 Master Data Service 配置管理器中的“Web 应用程序”，配置 Web 应用程序，然后单击“应用”将设置应用到 MDS。 请参阅图 23。 有关详细信息，请参阅 [Master Data Services 的安装和配置](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

    ![配置 Web 应用程序](media/Fig23_MDSWebApplication.png)

    图 23

    MDS 的安装已完成。 可重复上述步骤将 MDS 设置为在所有节点上运行。 同一 AG 上的后端数据库是相同的。

6.  如果之前为了创建 AlwaysOn AG 而创建了临时数据库（请参阅[创建可用性组](#create-an-availability-group)部分），则需要删除临时数据库

    有关 Master Data Service 的详细信息，请参阅 [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds)。

## <a name="conclusion"></a>结语

在此白皮书中，我们已了解如何在 SQL Server AlwaysOn 可用性组上设置并配置 Master Data Services 后端数据库。 此配置在 Master Data Services 后端数据库上提供高可用性和灾难恢复。 若要实现此配置，需要安装并配置 Windows Server 故障转移群集、SQL Server AlwaysOn 可用性组和 Master Data Services。

## <a name="feedback"></a>反馈

此白皮书对您有帮助吗？ 请单击文章顶部的“评论”向我们提供反馈。 

你的反馈将帮助我们改进所发布的白皮书质量。 

