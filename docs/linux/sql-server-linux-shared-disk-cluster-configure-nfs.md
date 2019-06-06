---
title: 配置故障转移群集实例存储 NFS-Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 0e325a8f717a84ed224fa619bdb47e79cf7af80f
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719357"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>配置 NFS-Linux 上的 SQL Server 的故障转移群集实例-

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置故障转移群集实例 (FCI) 的 NFS 存储。 

NFS 或网络文件系统，是用于共享在 Linux 领域，但未一个 Windows 中的磁盘的常见方法。 类似于 iSCSI，NFS 可以配置或某种形式的设备或存储单元的服务器上，只要它满足 SQL Server 的存储要求。

## <a name="important-nfs-server-information"></a>NFS 服务器的重要信息

托管 NFS （在 Linux 服务器或其他内容） 的源必须使用/符合版本 4.2 或更高版本。 早期版本不会使用 Linux 上的 SQL Server。

在配置 NFS 服务器上共享的文件夹，请确保它们遵循这些指导原则的常规选项：
- `rw` 若要确保该文件夹可以进行读取和写入
- `sync` 若要确保保证对该文件夹的写操作
- 不要使用`no_root_squash`作为一个选项; 它被视为安全风险
- 请确保该文件夹拥有完全控制权限 (777) 应用

请确保用于访问实施的安全标准。 当配置文件夹，请确保参与 FCI 服务器应该看到 NFS 文件夹。 在基于 Linux 的 NFS 解决方案修改 /etc/exports 的示例所示的文件夹是限制为 FCIN1 和 FCIN2。

![05-nfsacl][1]

## <a name="instructions"></a>Instructions

1. 在 FCI 配置中选择一个将加入的服务器。 并不重要哪一个。 

2. 检查以查看该服务器可以在 NFS 服务器上看到 mount(s)。

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址。

3. 对于系统数据库或存储在默认数据位置的任何内容，请执行以下步骤。 否则，请跳到步骤 4。
 
   * 请确保 SQL Server 已停止正在努力在服务器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 开关完全是超级用户。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   * 要使用 mssql 用户的开关。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   * 创建一个临时目录来存储 SQL Server 数据和日志文件。 如果成功，将不会收到任何确认。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 是文件夹的名称。 以下示例创建一个名为 /var/opt/mssql/tmp 文件夹。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * 将 SQL Server 数据和日志文件复制到临时目录。 如果成功，将不会收到任何确认。
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是上一步中的文件夹的名称。

   * 验证文件在目录中。

    ```bash
    ls TempDir
    ```

    \<TempDir > 是从步骤 d 文件夹的名称。

   * 从现有的 SQL Server 数据目录中删除的文件。 如果成功，将不会收到任何确认。

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * 验证已删除的文件。 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 若要切换回根用户的键入 exit。

   * 装载 NFS 共享的 SQL Server 数据文件夹中。 如果成功，将不会收到任何确认。

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址 

    \<FolderOnNFSServer > 是的 NFS 共享的名称。 下面的示例语法与步骤 2 中的 NFS 信息匹配。

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 检查以查看装载通过不带任何开关发出装入成功。

    ```bash
    mount
    ```

    ![10 mountnoswitches][2]

   * 切换到 mssql 用户。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   * 将文件从临时目录 /var/opt/mssql/data 复制。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 验证文件存在。

    ```bash
    ls /var/opt/mssql/data
    ```

   * 输入退出以不是 mssql 
    
   * 输入退出以不是根

   * 启动 SQL Server。 如果已正确复制所有内容和应用的安全设置是否正确，SQL Server 应显示为已启动。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 创建数据库，以测试已正确设置了安全。 下面的示例演示通过 TRANSACT-SQL; 完成这些操作后它可以通过 SSMS 完成。
 
    ![CreateTestdatabase][3]

   * 停止 SQL Server，并验证它关闭的情况下。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 如果不创建任何其他 NFS 装载，卸载共享。 如果是，不卸载。

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址

    \<FolderOnNFSServer > 是的 NFS 共享的名称

    \<FolderMountedIn > 是上一步中创建的文件夹。 

4. 为系统数据库，例如，用户数据库或备份以外的内容，请执行以下步骤。 如果只使用了默认位置，请跳到步骤 5。

   * 切换到是超级用户。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   * 创建 SQL Server 将使用的文件夹。 

    ```bash
    mkdir <FolderName>
    ```

    \<文件夹名 > 是文件夹的名称。 文件夹的完整路径需要指定如果不在正确的位置。 以下示例创建一个名为 /var/opt/mssql/userdata 文件夹。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 装载 NFS 共享上一步中创建的文件夹中。 如果成功，将不会收到任何确认。

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址

    \<FolderOnNFSServer > 是的 NFS 共享的名称

    \<FolderToMountIn > 是上一步中创建的文件夹。 下面是一个示例。 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 检查以查看装载通过不带任何开关发出装入成功。
  
   * 键入 exit 以不再是超级用户。

   * 若要测试，请在该文件夹中创建数据库。 以下示例使用 sqlcmd 创建数据库，将上下文切换到它，验证文件存在于 OS 级别，然后删除该临时位置。 可以使用 SSMS。

    ![15-createtestdatabase][4]
 
   * 卸载共享 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址
    
    \<FolderOnNFSServer > 是的 NFS 共享的名称

    \<FolderMountedIn > 是上一步中创建的文件夹。 下面是一个示例。 
 
5. 重复对其他节点的步骤。


## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
