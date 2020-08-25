---
title: 为 Linux 上的 SQL Server 部署 Pacemaker 群集
description: 了解如何为 SQL Server Always On 可用性组 (AG) 或故障转移群集实例 (FCI) 部署 Linux Pacemaker 群集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ebee4156a89a7eb2464abbda997f20a99be30753
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088917"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>为 Linux 上的 SQL Server 部署 Pacemaker 群集

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本教程列出了为 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Always On 可用性组 (AG) 或故障转移群集实例 (FCI) 部署 Linux Pacemaker 群集所需完成的任务。 与紧密耦合的 Windows Server/ [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 堆栈不同，Linux 上 Pacemaker 群集的创建和可用性组 (AG) 的配置可以在 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 安装之前或之后完成。 在配置完群集之后，才集成和配置 AG 或 FCI 部署的 Pacemaker 部分的资源。
> [!IMPORTANT]
> 群集类型为 None 的 AG 不需要 Pacemaker 群集，也不能由 Pacemaker 管理。 

> [!div class="checklist"]
> * 安装高可用性加载项并安装 Pacemaker。
> * 为 Pacemaker 准备节点（仅限 RHEL 和 Ubuntu）。
> * 创建 Pacemaker 群集。
> * 安装 SQL Server HA 和 SQL Server 代理包。
 
## <a name="prerequisite"></a>先决条件
[安装 SQL Server 2017](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>安装高可用性加载项
使用以下语法安装构成 Linux 每个分发的高可用性 (HA) 加载项的包。 

**Red Hat Enterprise Linux (RHEL)**
1.  使用以下语法注册服务器。 系统会提示输入有效的用户名和密码。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  列出可用的注册池。
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  运行以下命令，将 RHEL 高可用性与订阅相关联
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    其中，“PoolId”是上一步中高可用性订阅的池 ID。
    
4.  使存储库能够使用高可用性加载项。
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  安装 Pacemaker。
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

在 YaST 中安装高可用性模式或在服务器的主安装过程中执行此操作。 可以使用 ISO/DVD 作为源或将其联机来完成安装。
> [!NOTE]
> 在 SLES 上，创建群集时会初始化 HA 加载项。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>为 Pacemaker 准备节点（仅限 RHEL 和 Ubuntu）
Pacemaker 本身使用在名为 hacluster 的分发上创建的用户。 在 RHEL 和 Ubuntu 上安装 HA 加载项时，将创建用户。
1. 在将用作 Pacemaker 群集节点的每台服务器上，为群集使用的用户创建密码。 示例中使用的名称是 hacluster，但可以使用任何名称。 参与 Pacemaker 群集的所有节点上使用的名称和密码必须相同。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. 在将成为 Pacemaker 群集一部分的每个节点上，使用以下命令（RHEL 和 Ubuntu）启用并启动 `pcsd` 服务：

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   然后执行
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   以确保 `pcsd` 已启动。
3. 在 Pacemaker 群集的每个可能的节点上启用 Pacemaker 服务。
   
   ```bash
   sudo systemctl start pacemaker
   ```

   在 Ubuntu 上，会显示一个错误：
   
   *pacemaker Default-Start 未包含运行级别，正在中止。*
   
   此错误是一个已知问题。 尽管会出现该错误，但 Pacemaker 服务的启用是成功的，且此错误将在未来得到修复。
   
4. 接下来，创建并启动 Pacemaker 群集。 对于此步骤，RHEL 和 Ubuntu 之间存在一个区别。 虽然在这两个分发上，安装 `pcs` 会为 Pacemaker 群集配置默认配置文件，但在 RHEL 上，执行此命令会销毁任何现有配置并创建新群集。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>创建 Pacemaker 群集 
本节介绍如何为 Linux 的每个分发创建和配置群集。

**RHEL**

1. 为节点授权
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   其中 NodeX 是节点的名称。
2. 创建群集
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   其中 PMClusterName 是分配给 Pacemaker 群集的名称，Nodelist 是由空格分隔的节点名称列表 。

**Ubuntu**

Ubuntu 的配置与 RHEL 类似。 但有一个主要区别：安装 Pacemaker 包会为群集创建基本配置，并启用和启动 `pcsd`。 如果尝试通过严格遵循 RHEL 指令配置 Pacemaker 群集，会出现错误。 要解决此问题，请执行以下步骤： 
1. 从每个节点中删除默认的 Pacemaker 配置。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 按照 RHEL 部分中的步骤创建 Pacemaker 群集。

**SLES**

创建 Pacemaker 群集的过程在 SLES 上与在 RHEL 和 Ubuntu 上完全不同。 以下步骤展示如何使用 SLES 创建群集。
1. 通过在其中一个节点上运行 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   来启动群集配置过程。 系统可能会提示未配置 NTP 且未找到监视设备。 这没关系，依然能正常启动和运行。 如果使用基于存储的 SLES 内置隔离，则监视程序与 Stonith 相关。 可以稍后配置 NTP 和监视程序。
   
2. 系统会提示配置 Corosync。 系统会要求提供要绑定到的网络地址，以及多播地址和端口。 网络地址是你正在使用的子网，例如，192.191.190.0。 可以在每次提示时接受默认值，或在必要时进行更改。
   
3. 接下来，系统会询问是否要配置 SBD，即基于磁盘的隔离。 如果需要，可以在稍后完成此配置。 如果未配置 SBD，则与 RHEL 和 Ubuntu 不同的是，`stonith-enabled` 默认设置为 false。
   
4. 最后，系统会询问是否要配置用于管理的 IP 地址。 此 IP 地址是可选的，但功能类似于 Windows Server 故障转移群集 (WSFC) 的 IP 地址，因为它在群集中创建一个 IP 地址，将通过 HA Web Konsole (HAWK) 连接到该地址。 此配置也是可选的。
   
5. 确保群集已启动并运行，方法是发布 
   ```bash
   sudo crm status
   ```
   
6. 将 hacluster 密码更改为 
   ```bash
   sudo passwd hacluster
   ```
   
7. 如果为配置了用于管理的 IP 地址，可以在浏览器中对其进行测试，该过程同时还会测试 hacluster 的密码更改。
   ![hacLuster](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 在另一个将成为群集节点的 SLES 服务器上运行 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 出现提示时，输入在先前步骤中配置为群集的第一个节点的服务器的名称或 IP 地址。 将服务器添加为现有群集的节点。
   
10. 验证是否添加了节点，方法是发布 
   ```bash
   sudo crm status
   ```
   
11. 将 hacluster 密码更改为 
   ```bash
   sudo passwd hacluster
   ```
   
12. 对要添加到群集的所有其他服务器重复步骤 8-11。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>安装 SQL Server HA 和 SQL Server 代理包
如果尚未安装 SQL Server HA 包和 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理，请使用以下命令安装它们。 安装 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 后安装 HA 包需要重新启动 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 才能使用。 这些说明假定已经设置了 Microsoft 包的存储库，因为此时应安装 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。
> [!NOTE]
> - 如果不将 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 代理用于日志传送或任何其他用途，则不必安装它，这时可以跳过包 mssql-server-agent。
> - 其他用于 Linux 上的 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 全文搜索 (mssql-server-fts) 和 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (mssql-server-is) 的可选包对于高可用性、FCI 或 AG 都不是必需的 。

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>后续步骤

在本教程中，你学习了如何为 Linux 上的 SQL Server 部署 Pacemaker 群集。 你已了解如何执行以下操作：
> [!div class="checklist"]
> * 安装高可用性加载项并安装 Pacemaker。
> * 为 Pacemaker 准备节点（仅限 RHEL 和 Ubuntu）。
> * 创建 Pacemaker 群集。
> * 安装 SQL Server HA 和 SQL Server 代理包。

若要为 Linux 上的 SQL Server 创建和配置可用性组，请参阅：

> [!div class="nextstepaction"]
> [为 Linux 上的 SQL Server 创建和配置可用性组](sql-server-linux-create-availability-group.md)。

