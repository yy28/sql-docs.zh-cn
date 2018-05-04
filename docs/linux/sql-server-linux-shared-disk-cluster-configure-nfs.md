---
title: 配置故障转移群集实例存储 NFS-在 Linux 上的 SQL Server |Microsoft 文档
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: ddfc1b8546c97e8883730212300c331ed085b476
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>配置 NFS-在 Linux 上的 SQL Server 的故障转移群集实例-

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章介绍了如何在 Linux 上配置的故障转移群集实例 (FCI) 的 NFS 存储。 

NFS 或网络文件系统，是共享中 Linux world 但 Windows 一个磁盘的常见方法。 类似于 iSCSI，NFS 可以配置或某种形式的设备或存储单元的服务器上，只要它满足 SQL Server 的存储要求。

## <a name="important-nfs-server-information"></a>NFS 服务器的重要信息

承载 NFS （Linux 服务器或其他） 的源必须使用/符合 4.2 或更高版本。 早期版本不会使用在 Linux 上的 SQL Server。

配置 NFS 服务器上共享，请确保所文件夹时它们遵循以下这些准则常规选项：
- `rw` 若要确保文件夹可以进行读取和写入
- `sync` 若要确保保证对文件夹的写操作
- 不要使用`no_root_squash`作为一个选项; 它将被视为安全风险
- 请确保文件夹具有完全权限 (777) 应用

确保用于访问会实施安全标准。 当配置文件夹，请确保仅在 FCI 参与服务器应看到 NFS 文件夹。 对基于 Linux 的 NFS 解决方案修改 /etc/exports 的示例所示限于 FCIN1 和 FCIN2 文件夹的位置。

![05 nfsacl][1]

## <a name="instructions"></a>Instructions

1. 在 FCI 配置中选择一个将加入的服务器。 它并不重要哪一个。 

2. 检查服务器可以查看 mount(s)，NFS 服务器上。

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址。

3. 对于系统数据库或存储在默认数据位置的任何内容，请按照下列步骤。 否则，请跳到步骤 4。
 
   * 确保 SQL Server 已停止您正在使用的服务器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 完全要超级用户身份的开关。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   * 要 mssql 用户的开关。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   * 创建一个临时的目录来存储 SQL Server 数据和日志文件。 如果成功，将不会收到任何确认。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 是文件夹的名称。 下面的示例创建一个名为 /var/opt/mssql/tmp 文件夹。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * 将 SQL Server 数据和日志文件复制到临时目录。 如果成功，将不会收到任何确认。
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是前一步骤中的文件夹的名称。

   * 验证文件在目录中。

    ```bash
    ls TempDir
    ```

    \<TempDir > 是来自步骤 d 的文件夹的名称。

   * 从现有的 SQL Server 数据目录删除这些文件。 如果成功，将不会收到任何确认。

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * 验证文件已被删除。 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 键入 exit 以切换回根用户。

   * 装载 NFS 共享 SQL Server data 文件夹中。 如果成功，将不会收到任何确认。

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址 

    \<FolderOnNFSServer > 是 NFS 共享的名称。 下面的示例语法与步骤 2 中的 NFS 信息匹配。

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

   * 从临时目录 /var/opt/mssql/data 文件复制。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 验证文件存在。

    ```bash
    ls /var/opt/mssql/data
    ```

   * 输入 exit 不 mssql 
    
   * 输入 exit 不会是根

   * 启动 SQL Server。 如果正确复制的所有内容和应用安全设置是否正确，SQL Server 应显示为已启动。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 创建一个数据库以测试已正确设置了安全。 下面的示例演示正在通过 TRANSACT-SQL;它可以通过 SSMS 来完成。
 
    ![CreateTestdatabase][3]

   * 停止 SQL Server，并验证它关闭。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 如果你不在创建任何其他 NFS 装入，卸载共享。 如果你是，不卸载。

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址

    \<FolderOnNFSServer > 是 NFS 共享的名称

    \<FolderMountedIn > 是在上一步中创建的文件夹。 

4. 对于操作以外系统数据库，如用户数据库或备份，请按照这些步骤。 如果仅使用默认位置，请跳至步骤 5。

   * 为超级用户身份的开关。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   * 创建 SQL Server 将使用一个文件夹。 

    ```bash
    mkdir <FolderName>
    ```

    \<文件夹名称 > 是文件夹的名称。 该文件夹的完整路径，需要指定如果不在正确的位置。 下面的示例创建一个名为 /var/opt/mssql/userdata 文件夹。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 装载 NFS 共享上一步中创建的文件夹中。 如果成功，将不会收到任何确认。

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址

    \<FolderOnNFSServer > 是 NFS 共享的名称

    \<FolderToMountIn > 是在上一步中创建的文件夹。 下面是一个示例。 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 检查以查看装载通过不带任何开关发出装入成功。
  
   * 键入 exit 以不再是超级用户。

   * 若要测试，请在该文件夹中创建数据库。 下面的示例使用 sqlcmd 创建数据库，将上下文切换到它，验证文件中的操作系统级别中，存在，然后删除的临时位置。 你可以使用 SSMS。

    ![15-createtestdatabase][4]
 
   * 卸载共享 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是要使用 NFS 服务器的 IP 地址
    
    \<FolderOnNFSServer > 是 NFS 共享的名称

    \<FolderMountedIn > 是在上一步中创建的文件夹。 下面是一个示例。 
 
5. 重复的其他节点上的步骤。


## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
