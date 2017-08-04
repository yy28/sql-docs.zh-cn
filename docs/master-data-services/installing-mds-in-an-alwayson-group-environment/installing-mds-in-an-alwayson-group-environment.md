---
title: "高可用性和灾难恢复为 Master Data Services |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2afbf59101a0605dba2e79f09777160cb4de5cab
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>高可用性和灾难恢复为 Master Data Services

**摘要：** 本文介绍了一种解决方案，该解决方案适用于 AlwaysOn 可用性组配置上托管的 Master Data Service (MDS)。 本文介绍了如何在 SQL 2016 AlwaysOn 可用性组 (AG) 上安装和配置 SQL 2016 Master Data Services。 此解决方案的主要目的是改善 SQL Server 数据库上托管的 MDS 后端数据的高可用性和灾难恢复。

## <a name="introduction"></a>简介


本指南介绍了一种解决方案的主数据服务 (MDS) 位于 AlwaysOn 可用性组配置。 本文介绍如何安装和配置上的 SQL 2016 AlwaysOn 可用性组 (AG) 的 SQL 2016 MDS。 此解决方案的主要目的是改善 SQL Server 数据库上托管的 MDS 后端数据的高可用性和灾难恢复。

若要实现该解决方案，你需要完成以下任务本文中所述。

1.  [安装和设置 Windows Server 故障转移群集 (WSFC) 向上](#windows-server-failover-cluster-wsfc)。

2.  [设置 AlwaysOn 可用性组](#sql-server-alwayson-availability-group)。

3.  [配置在 WSFC 节点上运行的 MDS](#configure-mds-to-run-on-an-wsfc-node)。

前面几节将简要介绍的技术，跟说明。 有关的技术详细信息，请查看每个部分中链接的文档。

本文中所述此解决方案是基于 SQL Server AlwaysOn 可用性组，其中每个数据库都有多个同步或异步副本。 只有一个副本接受 （接受用户的请求） 的事务。 这是主副本。

每个副本都有其自己的存储，因此本解决方案中没有任何集中式的共享的存储。 如果没有软件故障，还是硬件故障影响主副本，您可以主副本的故障转移到同步或异步副本自动或手动取决于配置和情况。 这可确保对用户的最小中断与数据库的高可用性。

异步副本通常驻留在远离主副本的数据中心的数据中心上。 发生灾难情况下，主副本可以进行故障转移到另一个数据中心。 这可确保数据库进行灾难恢复。

出于演示目的，在本文中所述的解决方案使用以下版本的软件。 旧版本应工作相同，但有可能细微的差异。

-   使用服务器故障转移群集的 Windows Server 2012R2

-   与主数据服务功能的 SQL Server 2016

此外，解决方案使用两个 Vm， **MDS HA1**和**MDS HA2**，以承载两个副本。 只要它受支持 SQL Server AlwaysOn 可用性组，MDS 不限制可以使用的副本数。

本文假定你具有 Windows Server、 Windows Server 故障转移群集、 SQL Server AlwaysOn 和 SQL Server MDS 有关的基本知识。

## <a name="what-is-not-covered"></a>不包含的内容

本文档不涵盖以下：

-   如何使 IIS，web 服务器承载主数据服务 UI 中，高可用性和灾难后恢复。 MDS 不会施加任何特定的要求，在 IIS 中，以便使 IIS 高度可用和负载平衡的标准技术可以正常工作此处。

-   如何使用 SQL Server AlwaysOn 故障转移 (FCI) 群集来在 MDS 后端上支持高可用性 (HA)。 SQL Server 故障转移群集是不同的 HA 解决方案和正式支持的 SQL Server，并将与 MDS 正常运行。

-   如何使用 SQL Server 故障转移群集 (FCI) 和 AlwaysOn 可用性组的混合解决方案以在 MDS 后端上支持高可用性。 混合解决方案未使用 MDS。

## <a name="design-consideration"></a>设计注意事项

图 1 显示主要用于 AlwaysOn 可用性组的典型配置。 在主数据中心中，存在两个副本具有同步提交关系，并且两个副本必须投票特权。 这主要用于提高 HA，主副本失败的情况下。

在灾难恢复数据中心中，没有辅助副本具有与主异步提交关系。 此数据中心通常是不同于主数据中心的地理区域。 辅助副本不具有投票特权。

使用此配置以实现恢复，以防主数据中心灾难时，例如火灾、 地震，等等。配置均达到这两个高可用性和灾难恢复与相对较低的成本。

![AlwaysOn 可用性组的典型配置](media/Fig1_TypicalConfig.png)

图 1. 典型的 AlwaysOn 可用性组配置

如果你不需要考虑灾难恢复，你不必在第二个数据中心中具有的副本。 如果你需要提高 HA，然后你可以更多的同步副本中的同一主数据中心使用。

因此务必要考虑您的方案和要求，并选择多少异步和同步副本需要和的数据中心你应将它们放在。

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server 故障转移群集 (WSFC)

本部分介绍了以下任务。

1.  [安装 Windows 故障转移群集功能](#install-failover-cluster-feature)。

2.  [创建 Windows Server 故障转移群集](#create-a-windows-server-failover-cluster)。

上一节中的图 1 中所示，在本文中所述的解决方案包括 Windows Server 故障转移群集 (WSFC)。 我们需要设置 WSFC，因为 SQL AlwaysOn 依赖于 WFSC 用于故障检测和故障转移。

WSFC 是一项功能来提高应用程序和服务的高可用性。 它由一组组成的独立 windows 服务器实例使用 Microsoft 故障转移群集服务在这些实例上运行。 Windows 服务器实例 (或多个节点如有时称为) 连接，以便将它们可以相互之间进行通信，并且故障检测可能。 WSFC 提供故障检测和故障转移功能。 如果节点或服务失败群集中，然后检测到故障，并且另一个节点自动或手动开始提供在失败的节点上承载的服务。 在这种情况下，用户仅遇到在 services 中，最小中断和提高服务的可用性。  

### <a name="prerequisites"></a>必要條件

在所有实例上安装 Windows Server 操作系统和修补，则所有更新。

>[!NOTE] 
>它是**强烈建议**安装相同的 Windows 版本和相同的功能集的所有实例上，以避免任何潜在的不兼容性问题。

### <a name="install-failover-cluster-feature"></a>安装故障转移群集功能

完成以下步骤为每个 Windows 服务器实例可以在每个实例上安装 WSFC 功能。 你需要管理员权限。

1.  打开**服务器管理器**Windows Server，然后单击**添加角色和功能**右窗格中。 这将启动**添加角色和功能向导**。

2.  单击**下一步**直到你到达**功能**页。

3.  选择**故障转移群集**复选框，然后单击**下一步**以完成安装。 请参见图 2。

    如果系统询问你是否到确认**添加所需的故障转移群集的功能**，单击**添加功能**。 请参见图 3。

    ![添加角色和功能向导中，故障转移群集](media/Fig2_SelectFeatures.png)

    图 2

    ![添加角色和功能向导中，所需的故障转移群集](media/Fig3_RequiredFeaturesFailover.png)

    图 3

4.  上**确认**页上，单击**安装**安装故障转移群集功能。

5.  上**结果**页面上，确保所有内容已安装成功并且没有错误和警告。

### <a name="create-a-windows-server-failover-cluster"></a>创建 Windows Server 故障转移群集

在所有实例上安装了 WSFC 功能后，你可以配置 WSFC。 你应只需一个节点上执行此操作。

1.  打开**服务器管理器**Windows Server，然后单击**故障转移群集管理器**上**工具**在右上角启动管理器的菜单。

2.  在**故障转移群集管理器**，单击**验证配置**右窗格中。 请参见图 4。

    ![故障转移群集管理器中，验证配置](media/Fig4_ValidateConfig.png)

    图 4

3.  在**验证配置****向导**，单击**下一步**。

4.  在**选择服务器或群集**对话框框中，添加的服务器名称，将承载 SQL Server，然后单击**下一步**。 请参见图 5。

    在此示例中，我们将添加两个实例，MDS HA1 和 MDS HA2。

    ![验证配置向导，选择服务器或群集页](media/Fig5_AddServer.png)

    图 5

5.  上**测试选项**页上，单击**运行所有测试**，然后单击**下一步**。

6.  单击**下一步**完成验证。

    **验证**页将显示进度，和**摘要**页显示验证摘要。 请参阅图 6 和 7。

7.  上**摘要**页上，请检查是否任何警告或错误消息。

    必须修复错误。 但是，警告可能不是问题。 一条警告消息意味着"测试的项目可能满足的要求，但出现应检查"。 例如，图 7 显示"验证磁盘访问延迟"警告，这可能是由于临时，正在忙于在其他任务上的磁盘，你可能忽略它。 你应检查每个警告的联机文档和更多详细信息的错误消息。 请参阅图 7。
 
    ![验证配置向导中，验证页面](media/Fig6_ValidationTests.png)

    图 6

    ![验证配置向导，摘要页](media/Fig7_ValidationSummary.png)

    图 7

8.  上**摘要**页上，确认**现在使用已验证的节点创建群集**复选框已选中，然后单击**完成**启动**创建群集****向导**。

9.  在**创建群集****向导**，单击**下一步**。

10. 上**用于管理群集的访问点**页上，输入 WSFC 群集名称，然后单击**下一步**。 在此示例中，我们使用"MDS-HA"与群集同名。 请参阅图 8。

    ![输入群集名称](media/Fig8_EnterClusterName.png)

    图 8

11. 继续单击**下一步**以完成创建群集。 **摘要的群集 MDS-HA**部分显示的群集信息。 请参阅图 9。

    ![查看群集的摘要信息](media/Fig9_ClusterSummary.png)

    图 9

    如果您需要更高版本中添加节点，单击**添加节点**中的右窗格中的操作**故障转移群集管理器**。

注意：

-   WSFC 功能可能不在所有 Windows Server 版本上可用。 请确保你的版本具有此功能。

-   请确保你具有适当的权限设置 WSFC active directory 中。 如果有任何问题，请参阅[故障转移群集分步指南： 在 Active Directory 中配置帐户](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx)。

有关更多详细 WSFC 有关的信息，请参阅[故障转移群集](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx)。

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 可用性组

本部分介绍了以下任务。

1.  [启用 SQL Server AlwaysOn 可用性组](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)。

2.  [创建可用性组](#create-an-availability-group)。

3.  [验证和测试可用性组](#validation-and-test-the-availability-group)。

Sql Server AlwaysOn 解决方案为 sql Server 数据库提供高可用性和灾难恢复。 AlwaysOn 具有两个可能的解决方案。
是构建于 WSFC 之上。

-   AlwaysOn 可用性组 (AG)

-   AlwaysOn 故障转移群集实例 (FCI)。

可用性组增强了的数据库级高可用性。 可用性组 （组的用户数据库） 和其虚拟网络名称注册为 WSFC 中的资源。

FCI 可增强的实例级高可用性。 SQL Server 服务和相关的服务注册为 WSFC 中的资源。 此外，FCI 解决方案要求对称共享的磁盘存储，例如 SAN 或 SMB 文件共享，必须可供 WFC 群集中所有节点。


### <a name="prerequisites"></a>必要條件

-   在所有节点上安装 SQL Server。 有关详细信息，请参阅[安装 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server)。

-   （推荐）每个节点上安装的完全相同的 SQL Server 功能集和版本。 具体而言，必须安装 MDS。

-   （推荐）每个 SQL Server 实例上使用相同的配置。 具体而言，必须在所有 SQL Server 实例上配置相同的服务器排序规则。

-   （推荐）使用相同的服务帐户运行每个 SQL Server 实例。 否则，必须授予每个 SQL Server 实例上的权限，以确保 SQL Server 实例可以相互通信。

-   确认 Windows 防火墙设置允许与相互进行通信的 SQL Server 实例。

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>每个 SQL Server 实例上启用 SQL Server AlwaysOn 可用性组

1.  在**SQL Server 配置管理器**单击**SQL Server 服务**在左窗格中，右键单击**SQL Server**在右窗格中，然后单击**属性**。 请参阅图 10。

    ![SQL Server 属性窗口](media/Fig10_SQLServerProperties.png)

    图 10

2.  在**SQL Server (MSSQLSERVER)** **属性**对话框中，单击**AlwaysOn 高可用性**选项卡上，然后选择**启用 AlwaysOn 可用性组**复选框。 当一个值显示在**Windows 故障转移群集名称**文本框中，单击**确定**以继续。 请参阅图 11。

    ![启用 AlwaysOn 可用性组选项](media/Fig11_EnableAlwaysOn.png)

    图 11

3.  当显示一个警告页时，单击**确定**以继续。 请参阅图 12。

    ![确认停止并重新启动服务](media/Fig12_WarningServiceStopStart.png)

    图 12

4.  单击**重新启动**、 重新启动**SQL Server**服务并使此更改生效。 请参阅图 10。

>[!NOTE] 
>你可以更改运行 SQL Server 服务使用的服务帐户**SQL Server 配置管理器**。 单击**Log On**选项卡中**SQL Server (MSSQLSERVER)** **属性**对话框。 请参阅图 11。

### <a name="create-an-availability-group"></a>创建可用性组

在所有 SQL Server 实例启用 AlwaysOn 功能后，你将创建新的可用性组包含一个节点上的 MDS 数据库。

仅可以对现有数据库创建可用性组。 因此任一你在一个节点上创建 MDS 数据库或创建一个临时数据库，然后将放临时数据库。 在此示例中，我们将创建 emptyMDS 数据库，并在此 MDS 数据库中创建可用性组。

1.  启动**SQL Server Management Studio** (**SSMS**) 节点上，并连接到带有适当凭据的本地 SQL Server 实例。

2.  在 SSMS 中，打开**新查询**窗口并运行以下脚本以创建空数据库。 将 c： 替换\\临时位置与你想要用于执行完整备份。

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >完整数据库备份是用于在此数据库上创建可用性组所必需的。

3.  在**对象资源管理器**，展开**AlwaysOn 高可用性**文件夹，然后单击**新建可用性组向导**以启动**新建可用性组向导**。 请参阅图 13。

    ![启动新的可用性组向导](media/Fig13_AvailabilityGroupsFolder.png)

    图 13

4.  在**新的可用性组**向导中，单击**下一步**以显示**指定名称**页。 为可用性组中，键入一个名称，然后单击**下一步**。 请参阅图 14。

    ![输入可用性组的名称](media/Fig14_AvailabilityGroupName.png)

    图 14

5.  单击你刚刚在创建的数据库**选择数据库**页，，然后单击**下一步**。 请参阅图 15。

    ![选择的数据库](media/Fig15_AvailabilityGroupSelectDatabase.png)

    图 15

6.  上**指定副本**页上，通过单击来添加另一个副本**将副本添加**。 此页已为副本列出当前的本地 SQL Server 实例。 请参阅图 16。

7.  在**连接到服务器**对话框框中，添加适当的凭据并单击**连接**。

    ![连接到 SQL Server 实例](media/Fig16_AddReplicaConnectServer.png)

    图 16

    现在，你应看到在列表中的两个副本。 重复此步骤以将其他节点添加为副本。 请参阅图 17。

    ![副本的视图列表](media/Fig17_AvailabilityGroupSQLReplicas.png)

    图 17

    对于每个副本，配置以下各项**同步提交**，**自动故障转移**，和**可读辅助副本**设置。 请参阅图
17.

    **同步提交**： 这可确保，如果数据库的主副本上提交事务，然后还提交事务对所有其他同步副本。 异步提交不保证这一点，和它可能滞后于主副本。

    仅当两个节点处于同一数据中心时，通常应启用同步提交。 如果它们是在不同数据中心，同步提交可能会降低数据库的性能。

    如果未选中此复选框，则使用异步提交。

    **自动故障转移：**时主副本已关闭，可用性组将自动故障转移到其辅助副本选择自动故障转移时。 仅使用同步提交副本上启用此属性。

    **可读辅助副本：**默认情况下，用户无法连接到任何辅助副本。 这将使用户能够连接到具有只读访问权限的辅助副本。

8.  上**指定副本**页上，单击**侦听器**选项卡，执行以下。 请参阅图 18。

    a.  单击**创建可用性组侦听器**设置 MDS 数据库连接的可用性组侦听器。

    b.  输入**侦听器 DNS 名称**，如 MDSSQLServer。

    c.  在输入默认 SQL 端口 1433，**端口**文本框。

    d.  输入中的 DHCP**网络模式**文本中，然后单击**下一步**以继续。

    >[!NOTE] 
    >（可选） 你可以选择"静态 IP"作为**网络模式**并输入静态 IP。 你也可以输入 1433年以外的端口。 

    ![配置侦听器](media/Fig18_AvailabilityGroupCreateListener.png)

    图 18

9.  上**选择数据同步**页上，单击**完整**，并指定每个节点都能够访问的网络共享。 单击 **“下一步”** 继续。 请参阅图 19。

    此网络共享将用于存储要创建辅助副本的数据库备份。 如果这不是可供你组织的请选择另一个数据同步首选项。 请参阅[SQL Server 2016 AlwaysOn 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)如何使用其他选项来创建辅助副本。 图 17 还列出了其他选项。

    ![配置数据同步](media/Fig19_AvailabilityGroupDataSync.png)

    图 19 

10. 上**验证**页面上，确保所有验证都传递成功，并更正任何错误。 单击 **“下一步”** 继续。

11. 上**摘要**页上，查看所有配置设置，单击**完成**。 这将创建可用性组，并对其进行配置。

12. 上**结果**页上，确认已完成所有必需的步骤。

### <a name="validation-and-test-the-availability-group"></a>验证和测试可用性组

1.  打开 SSMS 并连接到你在中创建的侦听器 DNS 名称[创建可用性组](#create-an-availability-group)部分。 在此示例中，它是 MDSSQLServer。

2.  在**对象资源管理器**，展开**AlwaysOn 高可用性**文件夹中，右键单击你刚可用性组中创建[创建可用性组](#create-an-availability-group)部分，并依次**显示仪表板**。 请参阅图 20。 新的可用性组和其副本的状态将出现。

    ![查看仪表板](media/Fig20_ShowDashboard.png)

    图 20 

3.  单击**故障转移**以执行同步的副本和异步副本的故障转移。 这是为了验证发生正确该故障转移不会出现问题。

 完成 AlwaysOn 设置。

有关 AlwaysOn 可用性组的详细信息，请参阅[SQL Server 2016 AlwaysOn 可用性组](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)。

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>配置到 WSFC 节点上运行的 MDS

本文介绍此解决方案只需要在 WSFC 上运行的 MDS 后端数据库。 MDS，如 web 应用程序和 MDS 配置管理器中，其他部分可以在 WSFC 中或外部 WSFC 中，在节点上，只要 MDS 可以连接到可用性组上会运行。

1.  打开**主数据服务配置管理器**一个节点上，单击**数据库配置**，然后单击**Create Database**以启动**创建数据库向导**。

2.  上**数据库服务器**页上，键入中的可用性组侦听器 DNS 名称**SQL Server 实例**文本框中，单击**测试连接**，然后单击**下一步**。 请参阅图 21。

    ![使用可用性组侦听器配置数据库服务器](media/Fig21_MDSDatabaseServerListener.png)

    图 21

3.  上**数据库**页上，键入你在中创建数据库的名称[创建可用性组](#create-an-availability-group)部分，并依次**下一步**。 请参阅图 22。

    ![创建和配置数据库](media/Fig22_MDSCreateDatabase.png)

    图 22

4.  完成**创建数据库****向导**。 有关详细信息，请参阅[主数据服务安装和配置](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

5.  单击**Web 应用程序**中**主数据服务配置管理器**以配置 Web 应用程序，然后单击**应用**将设置应用于 MDS。 请参阅图 23。 有关详细信息，请参阅[主数据服务安装和配置](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

    ![配置 Web 应用程序](media/Fig23_MDSWebApplication.png)

    图 23

    MDS 安装程序完成。 你可以重复上述步骤以将 MDS 设置在所有节点上运行。 后端数据库是在同一个可用性组中相同。

6.  如果以前创建的临时数据库 (请参阅[创建可用性组](#create-an-availability-group)部分) 若要创建 AlwaysOn 可用性组，然后你应删除临时数据库

    有关主数据服务的详细信息，请参阅[Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds)。

## <a name="conclusion"></a>结语

在本白皮书，我们已了解如何设置和配置 Master Data Services 后端数据库基于 SQL Server AlwaysOn 可用性组。 此配置 Master Data Services 后端数据库上提供高可用性和灾难恢复。 若要实现此配置，你需要安装和配置 Windows Server 故障转移群集，SQL Server AlwaysOn 可用性组和 Master Data Services。

## <a name="feedback"></a>反馈

此白皮书对您有帮助吗？ 请向我们提供你的反馈通过单击**注释**文章顶部。 

你的反馈将帮助我们改进我们发布的白皮书的质量。 


