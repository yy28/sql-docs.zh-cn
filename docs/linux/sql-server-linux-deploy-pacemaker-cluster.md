---
title: Linux 上的 SQL Server 部署 Pacemaker 群集 |Microsoft Docs
description: 本教程演示如何为 Linux 上的 SQL Server 部署 Pacemaker 群集。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 239d4418c5e7d59a980d9028e2533dd9d7a2c566
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001829"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Linux 上的 SQL Server 部署 Pacemaker 群集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教程介绍如何部署 Linux Pacemaker 群集。 有关所需的任务[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Always On 可用性组 (AG) 或故障转移群集实例 (FCI)。 与不同的是紧密耦合的 Windows Server /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]之前或之后安装，可以完成堆栈、 创建 Pacemaker 群集，以及在 Linux 上的可用性组 (AG) 配置[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 集成和 Pacemaker 部分 AG 或 FCI 部署的资源的配置完成后对群集进行配置。
> [!IMPORTANT]
> 为无群集类型 AG does*不*要求 Pacemaker 群集，也不可以接受它受 Pacemaker。 

> [!div class="checklist"]
> * 安装高可用性外接程序并安装 Pacemaker。
> * 准备为 Pacemaker （RHEL 和仅适用于 Ubuntu） 的节点。
> * 创建 Pacemaker 群集。
> * 安装 SQL Server HA 和 SQL Server 代理包。
 
## <a name="prerequisite"></a>先决条件
[安装 SQL Server 2017](sql-server-linux-setup.md)。

## <a name="install-the-high-availability-add-on"></a>安装高可用性外接程序
使用以下语法来安装包组成的高可用性 (HA) 外接程序的每个 Linux 分发版。 

**Red Hat Enterprise Linux (RHEL)**
1.  使用以下语法将服务器注册。 系统提示您输入有效的用户名和密码。
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  列出用于注册的可用池。
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  运行以下命令以将 RHEL 高可用性与订阅相关联
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    其中*池 Id*是上一步中的高可用性订阅的池 ID。
    
4.  启用存储库，以便能够使用高可用性外接程序。
    
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

在 YaST 中安装高可用性模式或执行此操作的服务器的主安装的一部分。 可以使用 ISO/DVD 完成安装，为源或通过联机获取。
> [!NOTE]
> 在 SLES，创建群集时就会初始化 HA 加载项。

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>准备为 Pacemaker （RHEL 和仅适用于 Ubuntu） 的节点
Pacemaker 本身使用名为的分发上创建的用户*hacluster*。 RHEL 和 Ubuntu 上安装了 HA 加载项时，获取创建用户。
1. 每个服务器上将充当 Pacemaker 群集的节点，创建将由群集用户的密码。 在示例中使用的名称是*hacluster*，但可以使用任何名称。 名称和密码必须为相同参与 Pacemaker 群集的所有节点上。
   
    ```bash
    sudo passwd hacluster
    ```
    
2. 每个节点上将成为 Pacemaker 群集的一部分，启用并启动`pcsd`服务使用以下命令 （RHEL 和 Ubuntu）：

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

   Ubuntu 上你看到如下错误：
   
   *pacemaker 默认启动不包含运行级别，正在中止。*
   
   此错误是已知的问题。 即使出错，启用 Pacemaker 服务成功，并修复此 bug 将会在某一时刻在将来。
   
4. 接下来，创建并启动 Pacemaker 群集。 有一个区别是 RHEL 和 Ubuntu 在此步骤。 在这两个分布区上安装`pcs`Pacemaker 群集，在 RHEL、 执行此命令会销毁任何现有的配置会配置默认配置文件，并创建新群集。

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>创建 Pacemaker 群集 
本部分介绍如何创建和配置群集的每个 Linux 分发版。

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
   
   其中*PMClusterName*是分配给 Pacemaker 群集的名称和*Nodelist*是由空格分隔的节点的名称的列表。

**Ubuntu**

配置 Ubuntu 是类似于 RHEL。 但是，还有一个主要区别： 安装 Pacemaker 包创建的群集，并启用和启动的基本配置`pcsd`。 如果你尝试按照的 RHEL 完全配置 Pacemaker 群集，你将收到错误。 若要解决此问题，请执行以下步骤： 
1. 从每个节点中删除默认 Pacemaker 配置。
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. 按照创建 Pacemaker 群集 RHEL 部分中的步骤。

**SLES**

创建 Pacemaker 群集的过程是完全不同 SLES 上而不是 RHEL 和 Ubuntu。 以下步骤介绍如何使用 SLES 创建群集。
1. 首先运行群集配置过程 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   其中一个节点上。 未配置 NTP 和找到没有监视程序设备，系统可能提示您。 这是相当不错的事情启动并运行。 如果使用基于存储的 SLES 的内置隔离 STONITH 与监视器。 更高版本配置 NTP 和监视器。
   
2. 系统会提示要将 Corosync 配置。 系统会要求以要以及多播的地址和端口绑定到的网络地址。 网络地址是使用; 的子网例如，192.191.190.0。 可以接受在每个提示符下，默认值或根据需要更改。
   
3. 接下来，会要求你想要配置 SBD，这是基于磁盘的隔离。 如果需要，可以稍后执行此配置。 如果不是 SBD 配置，不同于在 RHEL 和 Ubuntu，`stonith-enabled`将默认情况下设置为 false。
   
4. 最后，会要求你想要配置管理的 IP 地址。 此 IP 地址是可选的但函数类似于 Windows Server 故障转移群集 (WSFC) 群集要用于连接到它通过 HA Web Konsole (HAWK) 中创建的 IP 地址在意义上的 IP 地址。 此配置中，也是可选的。
   
5. 确保群集已启动并运行通过发出 
   ```bash
   sudo crm status
   ```
   
6. 更改*hacluster*与密码 
   ```bash
   sudo passwd hacluster
   ```
   
7. 如果配置管理的 IP 地址，你可以测试它在浏览器还将检测更改的密码*hacluster*。
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. 另一个 SLES 服务器上将成为群集的节点，运行 
   ```bash
   sudo ha-cluster-join
   ```
   
9. 出现提示时，输入名称或 IP 地址的服务器的已配置为在上一步骤中的群集的第一个节点。 此服务器是作为节点添加到现有群集。
   
10. 验证通过发出添加节点 
   ```bash
   sudo crm status
   ```
   
11. 更改*hacluster*与密码 
   ```bash
   sudo passwd hacluster
   ```
   
12. 重复步骤 8 到 11 的所有其他服务器添加到群集。

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>安装 SQL Server HA 和 SQL Server 代理包
使用以下命令来安装 SQL Server HA 包和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]代理，如果它们没有已安装。 在安装后安装 HA 包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]需要重新启动[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，才能使用。 这些说明假定，Microsoft 包存储库已设置，因为[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]应在此处安装。
> [!NOTE]
> - 如果您将不使用[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]日志传送或任何其他使用代理，它没有安装，因此包*mssql server 代理*，可以跳过。
> - 有关其他可选包[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Linux 上，[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]全文搜索 (*mssql server fts*) 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Integration Services (*mssql server 是*)，不是所需的高可用性，为 FCI 或可用性组。

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

在本教程中，您学习了如何为 Linux 上的 SQL Server 部署 Pacemaker 群集。 你将了解到：
> [!div class="checklist"]
> * 安装高可用性外接程序并安装 Pacemaker。
> * 准备为 Pacemaker （RHEL 和仅适用于 Ubuntu） 的节点。
> * 创建 Pacemaker 群集。
> * 安装 SQL Server HA 和 SQL Server 代理包。

若要创建和配置 Linux 上的 SQL Server 可用性组，请参阅：

> [!div class="nextstepaction"]
> [创建和配置 Linux 上的 SQL Server 可用性组](sql-server-linux-create-availability-group.md)。

