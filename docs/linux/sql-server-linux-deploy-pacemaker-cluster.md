---
title: "在 Linux 上的 SQL Server 的部署 Pacemaker 群集 |Microsoft 文档"
description: "本教程演示如何在 Linux 上的 SQL Server 的部署 Pacemaker 群集。"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: dd9d35a7fa6e8a8a0e826d584a4f78ca2581d9bc
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的部署 Pacemaker 群集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍部署的 Linux Pacemaker 群集所需的任务[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Always On 可用性组 (AG) 或故障转移群集实例 (FCI)。 与紧密耦合的 Windows Server /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]堆栈、 Pacemaker 群集创建，以及在 Linux 上的可用性组 (AG) 配置，可以进行的安装之前或之后[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 集成和资源的可用性组或 FCI 部署 Pacemaker 部分配置完成后将该群集配置。
> [!IMPORTANT]
> 群集类型为一个可用性组未*不*要求 Pacemaker 群集中，也不可以管理它通过 Pacemaker。 

> [!div class="checklist"]
> * 安装高可用性外接程序并安装 Pacemaker。
> * 准备 Pacemaker （RHEL 和仅 Ubuntu） 的节点。
> * 创建 Pacemaker 群集。
> * 安装 SQL Server HA 和 SQL Server 代理包。
 
## <a name="prerequisite"></a>前提条件
[安装 SQL Server 自 2017 年](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>安装高可用性外接程序
使用以下语法来安装构成针对的每个分布的 Linux 的高可用性 (HA) 外接程序的包。 

**Red Hat Enterprise Linux (RHEL)**
1.  注册服务器使用以下语法。 系统提示您输入有效的用户名和密码。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  列出有关注册的可用池。
    
    ```bash
    sudo subscription-manager list --available
3.  Run the following command to associate RHEL high availability with the subscription
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    其中*池 Id*是前一步骤中的高可用性订阅的池 ID。
    
4.  启用要能够使用的高可用性外接程序的存储库。
    
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

在 YaST 中安装的高可用性模式，或者执行其作为主安装服务器的一部分。 可以完成 ISO/DVD 安装作为源或通过联机获取。
> [!NOTE]
> 在 SLES，创建群集时，获取初始化的 HA 外接程序。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>准备 Pacemaker （RHEL 和仅 Ubuntu） 的节点
Pacemaker 本身使用用户创建名为对分发*hacluster*。 RHEL 和 Ubuntu 上安装的 HA 外接程序时，获取创建该用户。
1. 在每个服务器上将充当 Pacemaker 群集的节点，创建群集要使用用户的密码。 在示例中使用的名称是*hacluster*，但可以使用任何名称。 名称和密码必须在参与 Pacemaker 群集中的所有节点上相同。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. 在将成为 Pacemaker 群集一部分的每个节点，请启用和启动`pcsd`服务使用以下命令 （RHEL 和 Ubuntu）：

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   然后执行
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   若要确保`pcsd`已启动。
3. 启用 Pacemaker 群集的每个可能的节点上的 Pacemaker 服务。
   
   ```bash
   sudo systemctl start pacemaker
   ```

   在 Ubuntu，你将看到如下错误：
   
   *pacemaker 默认启动包含没有运行，正在中止的级别。*
   
   此错误是已知的问题。 即使出错，启用 Pacemaker 服务成功，并且此 bug 将会修复某一时刻将来。
   
4. 接下来，创建并启动 Pacemaker 群集。 一个之间没有区别 RHEL 和 Ubuntu 在此步骤。 在这两种分发上安装`pcs`为 RHEL、 执行此命令上的 Pacemaker 群集销毁任何现有的配置中配置默认配置文件并创建新的群集。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>创建 Pacemaker 群集 
本部分介绍如何创建和配置的每个分布的 Linux 群集。

**RHEL**

1. 授权节点
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 … NodeN> -u hacluster
   ```
   
   其中*NodeX*是节点的名称。
2. 创建群集
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   其中*PMClusterName*是分配给 Pacemaker 群集的名称和*Nodelist*是以空格分隔的节点的名称的列表。

**Ubuntu**

配置 Ubuntu 是类似于 RHEL。 但是，没有一个主要区别： 安装 Pacemaker 包创建的群集，并启用和启动的基本配置`pcsd`。 如果你尝试按照的 RHEL 完全配置 Pacemaker 群集，则会出现错误。 若要修复此问题，请执行以下步骤： 
1. 从每个节点中删除默认 Pacemaker 配置。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 按照创建 Pacemaker 群集 RHEL 部分中的步骤。

**SLES**

用于创建 Pacemaker 群集的过程是完全不同上 SLES 相比 RHEL 和 Ubuntu。 下面的步骤介绍如何使用 SLES 创建群集。
1. 通过运行启动群集配置过程 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   上的节点之一。 未配置 NTP 以及找到任何监视器设备，可能会提示你。 这是特别适用于操作启动并运行的。 如果你使用基于存储的 SLES 的内置隔离，将与 STONITH 相关监视器。 NTP 和监视器可以在以后配置。
   
2. 系统会提示你配置 Corosync。 将要求要以及多播的地址和端口绑定到的网络地址。 网络地址是你使用; 的子网例如，192.191.190.0。 你可以接受默认设置在每个提示符处，或如有必要更改。
   
3. 接下来，将要求你是否你想要配置 SBD，这是基于磁盘的隔离。 如果需要，可以稍后执行此配置。 如果 SBD 不配置，与不同 RHEL 和 Ubuntu，`stonith-enabled`将默认情况下设置为 false。
   
4. 最后，则系统会要求你是否想要配置管理的 IP 地址。 此 IP 地址是可选的但函数类似于在它在要用于连接到它通过 HA Web Konsole (HAWK) 群集中创建 IP 地址的意义上的 Windows Server 故障转移群集 (WSFC) 的 IP 地址。 此配置，也是可选的。
   
5. 确保该群集通过发出是启动并正在运行 
   ```bash
   sudo crm status
   ```
   
6. 更改*hacluster*使用的密码 
   ```bash
   sudo passwd hacluster
   ```
   
7. 如果你配置管理的 IP 地址，你可以测试它在浏览器，还会测试的密码更改*hacluster*。
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 在将成为群集的节点的另一个 SLES 服务器上, 运行 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 出现提示时，输入的名称或 IP 地址的服务器的已配置为在前面的步骤中的群集的第一个节点。 服务器作为节点添加到现有群集。
   
10. 验证通过发出添加节点 
   ```bash
   sudo crm status
   ```
   
11. 更改*hacluster*使用的密码 
   ```bash
   sudo passwd hacluster
   ```
   
12. 重复步骤 8-11 的所有其他服务器添加到群集。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>安装 SQL Server HA 和 SQL Server 代理包
使用以下命令以安装 SQL Server HA 包和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理，如果它们未已安装。 安装之后安装 HA 包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，需要重新启动[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]为以便能够使用它。 这些说明假定，Microsoft 包的存储库已设置，因为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]应此时安装。
> [!NOTE]
> - 如果你将不会使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]日志传送或任何其他使用的代理，它无需安装，因此包*mssql server 代理*可以跳过。
> - 有关其他可选包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]的全文搜索 (*mssql server fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql 服务器是*)，不是所需的高可用性，FCI 或可用性组。

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

在本教程中，您学习了如何在 Linux 上的 SQL Server 的部署 Pacemaker 群集。 你应该了解一下如何到：
> [!div class="checklist"]
> * 安装高可用性外接程序并安装 Pacemaker。
> * 准备 Pacemaker （RHEL 和仅 Ubuntu） 的节点。
> * 创建 Pacemaker 群集。
> * 安装 SQL Server HA 和 SQL Server 代理包。

若要创建和配置可用性组在 Linux 上的 SQL server，请参阅：

> [!div class="nextstepaction"]
> [创建和配置可用性组在 Linux 上的 SQL Server 的](sql-server-linux-create-availability-group.md)。

