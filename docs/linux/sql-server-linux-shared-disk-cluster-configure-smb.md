---
title: 配置故障转移群集实例存储 SMB-在 Linux 上的 SQL Server |Microsoft 文档
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
ms.openlocfilehash: b762740be742aa2d716b9d354c26fe87bb170732
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>配置 SMB-在 Linux 上的 SQL Server 的故障转移群集实例-

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章介绍了如何在 Linux 上配置的故障转移群集实例 (FCI) 的 SMB 存储。 
 
在非 Windows 世界中，SMB 是通常称为作为通用 Internet 文件系统 (CIFS) 共享，通过 Samba 实现。 在 Windows 世界中，访问 SMB 共享完成这种方式： \\SERVERNAME\SHARENAME。 对于基于 Linux 的 SQL Server 安装，必须为一个文件夹装载 SMB 共享。

## <a name="important-source-and-server-information"></a>源和服务器的重要信息

下面是一些提示和成功使用 SMB 的说明：
- SMB 共享可以在 Windows、 Linux、 或甚至从为只要它使用 SMB 3.0 或更高版本的设备。 Samba 和 SMB 3.0 的详细信息，请参阅[SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) Samba 实现是否符合 SMB 3.0。
- SMB 共享应将高度可用。
- 必须将安全性设置正确在 SMB 共享上。 下面是从 /etc/samba/smb.conf，示例 SQLData1 其中是共享的名称。

![05 smbsource][1]

## <a name="instructions"></a>Instructions

1.  在 FCI 配置中选择一个将加入的服务器。 它并不重要哪一个。

2.  获取有关 mssql 用户的信息。

    ```bash
    sudo id mssql
    ```
    
    请注意 uid、 gid 和组。 

3. 执行 `sudo smbclient -L //NameOrIP/ShareName -U User`。

    \<NameOrIP > 是的 DNS 名称或承载的 SMB 共享的服务器的 IP 地址。

    \<共享名 > 是 SMB 共享的名称。 

4. 系统数据库或存储在默认数据位置的任何内容请按照下列步骤。 否则，请跳到步骤 5。 

   *    确保 SQL Server 已停止您正在使用的服务器上。
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    完全要超级用户身份的开关。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```

   *    要 mssql 用户的开关。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   *    创建一个临时的目录来存储 SQL Server 数据和日志文件。 如果成功，将不会收到任何确认。

    ```bash
    mkdir <TempDir>
    ```

    <TempDir> 是文件夹的名称。 下面的示例创建一个名为 /var/opt/mssql/tmp 文件夹。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   *    将 SQL Server 数据和日志文件复制到临时目录。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是前一步骤中的文件夹的名称。
    
   *    验证文件在目录中。

    ```bash
    ls <TempDir>
    ```

    \<TempDir > 是来自步骤 d 的文件夹的名称。
    
   *    从现有的 SQL Server 数据目录删除这些文件。 如果成功，将不会收到任何确认。
 
    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    验证文件已被删除。 

    ```bash
    ls /var/opt/mssql/data
    ```
 
   *    键入 exit 以切换回根用户。

   *    安装 SQL Server data 文件夹中的 SMB 共享。 如果成功，将不会收到任何确认。 此示例演示用于连接到基于 Windows Server 的 SMB 3.0 共享的语法。

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<服务器名称 > 是 SMB 共享的服务器的名称
    
    \<共享名 > 是共享的名称

    \<用户名 > 是要访问该共享的用户的名称

    \<密码 > 是用户的密码

    \<域 > 是 Active Directory 的名称

    \<mssqlUID > 是的 mssql 用户 UID 
 
    \<mssqlGID > 是的 mssql 用户 GID
 
   *    检查以查看装载通过不带任何开关发出装入成功。

    ```bash
    mount
    ```
 
   *    切换到 mssql 用户。 如果成功，将不会收到任何确认。

    ```bash
    su mssql
    ```

   *    从临时目录 /var/opt/mssql/data 文件复制。 如果成功，将不会收到任何确认。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssql/data
    ```

   *    验证文件存在。

    ```bash
    ls /var/opt/mssql/data
    ```

   *    输入 exit 不 mssql 

   *    输入 exit 不会是根

   *    启动 SQL Server。 如果正确复制的所有内容和应用安全设置是否正确，SQL Server 应显示为已启动。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
 
   *    若要进一步测试，创建数据库，以确保是完好的权限。 下面的示例使用 Transact SQL;你可以使用 SSMS。

    ![10_testcreatedb][2] 
  
   *    停止 SQL Server，并验证它关闭。 如果想要添加或测试其他磁盘，请不关闭 SQL Server 那些添加和测试之前。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    仅当完成后，卸载共享。 否则，在完成测试/添加任何其他磁盘后卸载。

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
    ```

    \<IPAddressOrServerName > 是的 IP 地址或 SMB 主机的名称

    \<共享名 > 是共享的名称
    
    \<FolderMountedIn > 是 SMB 装载的文件夹的名称

5.  对于操作以外系统数据库，如用户数据库或备份，请按照这些步骤。 如果仅使用默认位置，请跳至步骤 14。
    
   *    为超级用户身份的开关。 如果成功，将不会收到任何确认。

    ```bash
    sudo -i
    ```
    
   *    创建 SQL Server 将使用一个文件夹。 

    ```bash
    mkdir <FolderName>
    ```

    \<文件夹名称 > 是文件夹的名称。 该文件夹的完整路径，需要指定如果不在正确的位置。 下面的示例创建一个名为 /var/opt/mssql/userdata 文件夹。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    安装 SQL Server data 文件夹中的 SMB 共享。 如果成功，将不会收到任何确认。 此示例演示用于连接到基于 Samba 的 SMB 3.0 共享的语法。

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<服务器名称 > 是 SMB 共享的服务器的名称

    \<共享名 > 是共享的名称

    \<文件夹名称 > 是最后一步中创建的文件夹的名称  

    \<用户名 > 是要访问该共享的用户的名称

    \<密码 > 是用户的密码

    \<mssqlUID > 是的 mssql 用户 UID

    \<mssqlGID > 是的 mssql 用户 GID。
 
   * 检查以查看装载通过不带任何开关发出装入成功。
 
   * 键入 exit 以不再是超级用户。

   * 若要测试，请在该文件夹中创建数据库。 下面的示例使用 sqlcmd 创建数据库，将上下文切换到它，验证文件中的操作系统级别中，存在，然后删除的临时位置。 你可以使用 SSMS。
 
   * 卸载共享 

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
    ```
    
    \<IPAddressOrServerName > 是的 IP 地址或 SMB 主机的名称
 
    \<共享名 > 是共享的名称
 
    \<FolderMountedIn > 是 SMB 装载的文件夹的名称。
 
6.  重复的其他节点上的步骤。

现在你就可以配置 FCI。

## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
