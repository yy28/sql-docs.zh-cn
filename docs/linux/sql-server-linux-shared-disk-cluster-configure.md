---
title: 配置故障转移群集实例的 SQL Server 上 Linux (RHEL) |Microsoft 文档
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 2550c2d53f50f2c5647ed0ab61d4d73e586495e2
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323958"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>配置故障转移群集实例的 SQL Server 上 Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 两个节点共享的磁盘故障转移群集实例提供高可用性的服务器级冗余。 在本教程中，您将学习如何在 Linux 上创建 SQL Server 的双节点故障转移群集实例。 你将完成的特定步骤包括：

> [!div class="checklist"]
> * 设置和配置 Linux
> * 安装和配置 SQL Server
> * 配置主机文件
> * 配置共享的存储并移动数据库文件
> * 在每个群集节点上安装和配置 Pacemaker
> * 配置故障转移群集实例

此文章介绍了如何为 SQL Server 中创建两个节点共享的磁盘故障转移群集实例 (FCI)。 本文章包括说明和脚本示例的 Red Hat Enterprise Linux (RHEL)。 Ubuntu 分发是类似于 RHEL，因此脚本示例将通常还在 Ubuntu 上工作。 

概念信息，请参阅[SQL Server 故障转移群集实例 (FCI) 在 Linux 上](sql-server-linux-shared-disk-cluster-concepts.md)。

## <a name="prerequisites"></a>必要條件

若要完成以下的端到端方案，你需要两台计算机部署两个节点群集和另一个服务器作为存储。 以下步骤概述了如何配置这些服务器。

## <a name="set-up-and-configure-linux"></a>设置和配置 Linux

第一步是在群集节点上配置操作系统。 在群集中的每个节点上配置 linux 分发。 在这两个节点上使用相同的分发和版本。 使用一个或多个以下的分发：
    
* RHEL HA 外接程序的有效订阅

## <a name="install-and-configure-sql-server"></a>安装和配置 SQL Server

1. 在这两个节点上设置 SQL Server 和安装。  有关详细说明，请参阅[在 Linux 上安装 SQL Server](sql-server-linux-setup.md)。
1. 出于配置目的，请将一个节点指定为主要节点，而将另一个指定为辅助节点。 使用以下术语，按照此指南操作。  
1. 在辅助节点上，停止并禁用 SQL Server。
    以下示例将停止并禁用 SQL Server： 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 在设置时，生成的 SQL Server 实例和放置在服务器 Master Key `var/opt/mssql/secrets/machine-key`。 在 Linux 上，SQL Server 始终以名为 mssql 的本地帐户身份运行。 因为它是本地帐户，所以其标识不会在节点之间共享。 因此，需要将加密密钥从主节点复制到每个辅助节点，以便每个本地 mssql 帐户均可访问它，从而解密服务器主密钥。 

1.  在主节点上，为 Pacemaker 创建的 SQL server 登录名和授予登录权限运行`sp_server_diagnostics`。 Pacemaker 使用此帐户来验证哪些节点正在运行 SQL Server。 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   连接到 SQL Server`master`数据库使用 sa 帐户，并运行以下命令：

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   或者，可以在更精细的级别设置权限。 Pacemaker 登录需要`VIEW SERVER STATE`到查询运行状况状态的 sp_server_diagnostics，`setupadmin`和`ALTER ANY LINKED SERVER`以通过运行 sp_dropserver 和 sp_addserver 在资源名称更新 FCI 实例名称。 

1. 在主节点上，停止并禁用 SQL Server。 

## <a name="configure-the-hosts-file"></a>配置主机文件

每个群集节点上，配置的主机文件。 主机文件必须包括 IP 地址和每个群集节点的名称。

1. 检查每个节点的 IP 地址。 以下脚本显示当前节点的 IP 地址。 

    ```bash
    sudo ip addr show
    ```

1. 在每个节点上设置计算机名。 为每个节点提供长度不超过 15 个字符的唯一名称。 将计算机名称设置通过将其添加到`/etc/hosts`。 以下脚本可使用 `vi` 编辑 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```
   下面的示例演示`/etc/hosts`名为的两个节点的添加`sqlfcivm1`和`sqlfcivm2`。

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>配置存储 （&) 移动数据库文件  

你需要提供两个节点都可以访问的存储。 你可以使用 iSCSI、 NFS 或 SMB。 配置存储，存储都呈现给群集节点，然后将数据库文件移动到新存储。 以下文章说明了每个存储类型的步骤：

- [配置故障转移群集实例-iSCSI-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [配置 NFS-在 Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [配置 SMB-在 Linux 上的 SQL Server 的故障转移群集实例-](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每个群集节点上安装和配置 Pacemaker

1. 在两个群集节点上，创建一个文件来存储用于 Pacemaker 登录的 SQL Server 用户名和密码。 

    以下命令创建并填充此文件：

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. 在两个群集节点上，打开 Pacemaker 防火墙端口。 若要使用 `firewalld` 打开这些端口，请运行以下命令：

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
1. 为安装 Pacemaker 和 Corosync 包时创建的默认用户设置密码。 在两个节点上使用相同的密码。 

   ```bash
   sudo passwd hacluster
   ```
1. 启用并启动 `pcsd` 服务和 Pacemaker。 这样，节点将可以在重新启动后重新加入群集。 在两个节点上运行以下命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. 为 SQL Server 安装 FCI 资源代理。 在两个节点上运行以下命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>配置故障转移群集实例

FCI 将创建资源组中。 由于资源组后，就不必约束，这是稍微容易些。 但是，将资源添加到他们应启动顺序中的资源组。 它们应启动的顺序是： 

1. 存储资源
2. 网络资源
3. 应用程序资源

此示例将创建 FCI 组 NewLinFCIGrp 中。 资源组的名称必须是唯一从在 Pacemaker 中创建任何资源。

1.  创建的磁盘资源。 如果不是问题，你将获得无响应。 若要创建的磁盘资源的方式取决于存储类型。 下面是一个示例，用于每个存储类型。 使用适用于群集存储的存储类型的示例。

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > 是的 iSCSI 磁盘与关联的资源的名称

    \<VolumeGroupName > 是的卷组的名称  

    \<LogicalVolumeName > 是的名称创建的逻辑卷  

    \<FolderToMountiSCSIDIsk > 是要安装的磁盘的文件夹 （对于系统数据库的默认位置，它将为 /var/opt/mssql/data）

    \<FileSystemType > EXT4，或者将 XFS 具体取决于如何操作的格式设置和哪些分发支持。 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > 是 NFS 共享与关联的资源的名称

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址

    \<FolderOnNFSServer > 是 NFS 共享的名称

    \<FolderToMountNFSShare > 是要安装的磁盘的文件夹 （对于系统数据库的默认位置，它将为 /var/opt/mssql/data）

    下面显示了一个示例：

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<服务器名称 > 是 SMB 共享的服务器的名称

    \<共享名 > 是共享的名称

    \<文件夹名称 > 是最后一步中创建的文件夹的名称
    
    \<用户名 > 是要访问该共享的用户的名称

    \<密码 > 是用户的密码

    \<ADDomain > 是 AD DS 域 （如果使用基于 Windows Server 的 SMB 共享时适用）

    \<mssqlUID > 是的 mssql 用户 UID

    \<mssqlGID > 是的 mssql 用户 GID

    \<RGName > 是资源组的名称
 
2.  创建将由 FCI 的 IP 地址。 如果不是问题，你将获得无响应。

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > 是的 IP 地址与关联的资源的名称

    \<Ip 地址 > 变量供 FCI 的 IP 地址

    \<NetworkCard > 是与子网 (即 eth0) 关联的网络卡

    \<子网掩码 > 是子网 (即 24) 的网络掩码

    \<RGName > 是资源组的名称
 
3.  创建 FCI 资源。 如果不是问题，你将获得无响应。

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > 是的名称的资源，不仅能与 FCI 相关联的友好名称。 这是什么用户和应用程序将用于连接。 

    \<RGName > 是资源组的名称。
 
4.  运行命令`sudo pcs resource`。 FCI 应处于联机状态。
 
5.  连接到使用 SSMS 或使用 FCI 的 DNS/资源名称的 sqlcmd FCI。

6.  发出语句`SELECT @@SERVERNAME`。 它应返回在 FCI 的名称。

7.  发出语句`SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`。 它应返回在运行 FCI 的节点的名称。

8.  手动故障 FCI 到其他节点。 请参阅下的说明操作[操作故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)。

9.  最后，故障回复到原始节点 FCI 并删除归置约束。

<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
-->
## <a name="summary"></a>“摘要”

在本教程中，你将完成以下任务。

> [!div class="checklist"]
> * 设置和配置 Linux
> * 安装和配置 SQL Server
> * 配置主机文件
> * 配置共享的存储并移动数据库文件
> * 在每个群集节点上安装和配置 Pacemaker
> * 配置故障转移群集实例

## <a name="next-steps"></a>后续步骤

- [运行故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
