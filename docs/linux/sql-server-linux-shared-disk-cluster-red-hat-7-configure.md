---
title: 为 SQL Server 配置 Red Hat Enterprise Linux 共享的群集 |Microsoft 文档
description: 为 SQL Server 配置 Red Hat Enterprise Linux 共享的磁盘群集实现高可用性。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: bbeeff135edbc333b6ce8b3e20cf5235710f2dc1
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677676"
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>配置适用于 SQL Server 的 Red Hat Enterprise Linux 共享磁盘群集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本指南介绍如何为 Red Hat Enterprise Linux 上的 SQL Server 创建两节点共享磁盘群集。 群集层基于 Red Hat Enterprise Linux (RHEL) 上[HA 加载项](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)基础上构建[Pacemaker](https://clusterlabs.org/)。 SQL Server 实例在一个节点或另一个节点上处于活动状态。

> [!NOTE] 
> 对 Red Hat HA 加载项和文档的访问需要一个订阅。 

如以下关系图所示，存储将呈现给两个服务器。 群集组件 - Corosync 和 Pacemaker - 协调通信和资源管理。 一台服务器具有到存储资源和 SQL Server 的活动连接。 当 Pacemaker 检测到故障时，群集组件负责管理将资源移到另一个节点。  

![Red Hat Enterprise Linux 7 共享磁盘的 SQL 群集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

有关群集配置、 资源代理选项和管理的详细信息，请访问[RHEL 参考文档](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。


> [!NOTE] 
> 这种情况下，SQL Server 与 Pacemaker 的集成不及与 Windows 版的 WSFC 集成的耦合性高。 在 SQL 内部，无法了解到群集是否存在，所有业务流程都是由外至内，并且 Pacemaker.将该服务作为一个独立实例控制。 此外例如，群集 dmv sys.dm_os_cluster_nodes 和 sys.dm_os_cluster_properties 将无任何记录。
若要使用指向字符串服务器名称的连接字符串而不使用 IP，他们将需要注册其 DNS 服务器中创建虚拟 IP 资源 （如以下各节中所述） 所使用的 IP 与所选的服务器名称。

以下各部分介绍了设置故障转移群集解决方案的步骤。 

## <a name="prerequisites"></a>必要條件

若要完成以下端到端方案，需要两台计算机部署两个节点群集和另一台服务器，若要配置 NFS 服务器。 以下步骤概述了如何配置这些服务器。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>在每个群集节点上安装和配置操作系统

第一步是在群集节点上配置操作系统。 对于此演练，将 RHEL 用于 HA 加载项的有效订阅。 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>在每个群集节点上安装和配置 SQL Server

1. 在两个节点上安装和设置 SQL Server。  有关详细说明，请参阅[Linux 上安装 SQL Server](sql-server-linux-setup.md)。

1. 出于配置目的，请将一个节点指定为主要节点，而将另一个指定为辅助节点。 使用以下术语，按照此指南操作。  

1. 在辅助节点上，停止并禁用 SQL Server。

   以下示例将停止并禁用 SQL Server： 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> 为 SQL Server 实例生成并放置在一个服务器主密钥在安装时`/var/opt/mssql/secrets/machine-key`。 在 Linux 上，SQL Server 始终以名为 mssql 的本地帐户身份运行。 因为它是本地帐户，所以其标识不会在节点之间共享。 因此，需要将加密密钥从主节点复制到每个辅助节点，以便每个本地 mssql 帐户均可访问它，从而解密服务器主密钥。 

1. 在主节点上为 Pacemaker 创建 SQL server 登录名并授予登录权限以运行`sp_server_diagnostics`。 Pacemaker 使用此帐户来验证哪个节点正在运行 SQL Server。 

   ```bash
   sudo systemctl start mssql-server
   ```

   连接到 SQL Server`master`使用 sa 帐户数据库并运行以下命令：

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   或者，可以在更精细的级别设置权限。 Pacemaker 登录需要`VIEW SERVER STATE`sp_server_diagnostics，与查询运行状况状态`setupadmin`和`ALTER ANY LINKED SERVER`通过运行 sp_dropserver 和 sp_addserver 使用的资源名称更新 FCI 实例名称。 

1. 在主节点上，停止并禁用 SQL Server。 

1. 配置每个群集节点的主机文件。 主机文件必须包含每个群集节点的 IP 地址和名称。 

    检查每个节点的 IP 地址。 以下脚本显示当前节点的 IP 地址。 

   ```bash
   sudo ip addr show
   ```

   在每个节点上设置计算机名。 为每个节点提供长度不超过 15 个字符的唯一名称。 通过将其添加到设置的计算机名称`/etc/hosts`。 以下脚本可使用 `vi` 编辑 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```
   下面的示例演示`/etc/hosts`并补充了两个名节点`sqlfcivm1`和`sqlfcivm2`。

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

在下一节中，将配置共享存储并且会将数据库文件移到该存储。 

## <a name="configure-shared-storage-and-move-database-files"></a>配置共享存储并移动数据库文件 

有多种解决方案可用于提供共享存储。 本演练演示如何使用 NFS 配置共享存储。 我们建议您遵循最佳做法，并使用 Kerberos 保护 NFS (您可以找到这里举个例子： https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/)。 

>[!Warning]
>如果不保护 NFS，然后将能够访问你的数据文件的任何人可以访问你的网络和欺骗 SQL 节点的 IP 地址。 与往常一样，请确保在将系统投入生产前，对系统建立威胁模型。 另一种存储方法是使用 SMB 文件共享。

### <a name="configure-shared-storage-with-nfs"></a>使用 NFS 配置共享的存储

> [!IMPORTANT] 
> 托管版本的 NFS 服务器上的数据库文件 < 4 不支持此版本中。 这包括使用共享的磁盘故障转移群集以及数据库在非群集实例上的 NFS。 我们正在努力实现其他 NFS 服务器版本中即将发布的版本。 

NFS 服务器上执行以下步骤：

1. 安装 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 启用和启动 `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. 启用和启动 `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  编辑`/etc/exports`导出你想要共享的目录。 您希望每个共享需要 1 行。 例如： 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. 导出共享

   ```bash
   sudo exportfs -rav
   ```

1. 验证路径是否为已共享/已导出，从 NFS 服务器运行

   ```bash
   sudo showmount -e
   ```

1. 在 SELinux 中添加异常

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. 打开服务器防火墙。

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>配置所有群集节点，以连接到 NFS 共享存储

执行以下步骤在所有群集节点上。

1.  安装 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 打开客户端和 NFS 服务器上的防火墙

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. 验证是否可以在客户端计算机上看到 NFS 共享

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. 对所有群集节点重复这些步骤。

有关如何使用 NFS 的详细信息，请参阅以下资源：

* [NFS 服务器和 firewalld |Stack Exchange](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [装载 NFS 卷 |Linux 网络管理员指南](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [NFS 服务器配置](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/3/html/Reference_Guide/s1-nfs-server-export.html)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>装载数据库文件目录，指向共享存储

1.  **仅在主节点上**，将数据库文件保存到临时位置。以下脚本，创建一个新的临时目录，将数据库文件复制到新的目录中删除旧的数据库文件。 以本地用户 mssql 身份运行 SQL Server 时，需要确保将数据传输到装载的共享后，本地用户对共享具有读写权限。 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  在所有群集节点上编辑`/etc/fstab`文件以包括装载命令。  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   以下脚本说明此类编辑的一个示例。  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>如果使用文件系统 (FS) 资源的建议此处，，则无需保留 /etc/fstab 中的装载命令。 Pacemaker 将负责在启动 FS 群集资源时装载文件夹。 帮助隔离的情况下，它将确保永远不会两次装载 FS。 

1.  运行`mount -a`命令获取系统来更新已装载的路径。  

1.  保存到的数据库和日志文件复制`/var/opt/mssql/tmp`到新装载的共享`/var/opt/mssql/data`。 这只需要完成**主节点上**。 请确保为 mssql 本地用户授予读的写权限。

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  验证 SQL Server 是否已成功通过新文件路径启动。 对每个节点均执行此操作。 此时，一次应只有一个节点运行 SQL Server。 它们不能同时运行，因为两者将同时尝试访问数据文件（要避免同时在两个节点上意外启动 SQL Server，请使用文件系统群集资源来确保共享未由不同的节点装载两次）。 以下命令可启动 SQL Server，检查状态，然后停止 SQL Server。
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
此时，SQL Server 的两个实例均已配置为使用共享存储上的数据库文件运行。 下一步，为 Pacemaker 配置 SQL Server。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每个群集节点上安装和配置 Pacemaker


2. 在两个群集节点上，创建一个文件来存储用于 Pacemaker 登录的 SQL Server 用户名和密码。 以下命令创建并填充此文件：

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 在两个群集节点上，打开 Pacemaker 防火墙端口。 若要使用 `firewalld` 打开这些端口，请运行以下命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 如果使用的是没有内置高可用性配置的其他防火墙，则需要打开以下端口，Pacemaker 才能与群集中的其他节点通信
   >
   > * TCP：端口 2224、3121、21064
   > * UDP：端口 5405

1. 在每个节点上安装 Pacemaker 包。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. 为安装 Pacemaker 和 Corosync 包时创建的默认用户设置密码。 在两个节点上使用相同的密码。 

   ```bash
   sudo passwd hacluster
   ```

   

3. 启用并启动 `pcsd` 服务和 Pacemaker。 这样，节点将可以在重新启动后重新加入群集。 在两个节点上运行以下命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 为 SQL Server 安装 FCI 资源代理。 在两个节点上运行以下命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="create-the-cluster"></a>创建群集 

1. 在其中一个节点上创建群集。

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 …> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 …>
   sudo pcs cluster start --all
   ```

   > RHEL HA 加载项具有 VMWare 和 KVM 的隔离代理。 需要在所有其他虚拟机监控程序上禁用隔离。 不建议在生产环境中禁用隔离代理。 截至时间范围内，有 HyperV 或云环境中的隔离代理。 如果正在运行其中一种配置，您需要禁用隔离。 \**建议不要在生产系统中 ！**

   以下命令禁用隔离代理。

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. 为 SQL Server、文件系统和虚拟 IP 资源配置群集资源，并将配置推送到群集。 您需要以下信息：

   - **SQL Server 资源名称**： 群集的 SQL Server 资源的名称。 
   - **浮动 IP 资源名称**： 虚拟 IP 地址资源的名称。
   - **IP 地址**： 客户端将用于连接到 SQL Server 的群集实例的 IP 地址。 
   - **文件系统资源名称**： 文件系统资源的名称。
   - **设备**: NFS 共享路径
   - **设备**： 装载到共享的本地路径
   - **fstype**： 文件共享类型 (例如 nfs)

   更新以下脚本为您的环境中的值。 在一个节点上运行，以配置并启动群集服务。  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   例如，以下脚本将创建一个名为的 SQL Server 群集资源`mssqlha`，并使用 IP 地址的浮动 IP 资源`10.0.0.99`。 它还可创建一个文件系统资源并添加约束，将所有资源并置到同一节点上作为 SQL 资源。 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   推送配置后，将在一个节点上启动 SQL Server。 

3. 验证 SQL Server 是否已启动。 

   ```bash
   sudo pcs status 
   ```

   以下示例展示了 Pacemaker 已成功启动 SQL Server 的群集实例时的结果。 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>其他资源

* [从头开始群集](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)pacemaker 的指南

## <a name="next-steps"></a>后续步骤

[Red Hat Enterprise Linux 共享的磁盘群集上运行 SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
