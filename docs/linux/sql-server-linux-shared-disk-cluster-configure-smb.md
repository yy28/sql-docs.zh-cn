---
title: 配置故障转移群集实例存储 SMB-Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7a8df4121fa71580af9596c855e0f0d6199fca46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712866"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>配置 SMB-Linux 上的 SQL Server 的故障转移群集实例-

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上配置故障转移群集实例 (FCI) 的 SMB 存储。 
 
在非 Windows 世界中，SMB 通常称为作为通用 Internet 文件系统 (CIFS) 共享和通过 Samba 实现。 在 Windows 世界中，访问 SMB 共享进行这种方式：\\SERVERNAME\SHARENAME. 对于基于 Linux 的 SQL Server 安装，必须为文件夹装载 SMB 共享。

## <a name="important-source-and-server-information"></a>源服务器和服务器的重要信息

下面是一些提示和说明，了解成功使用 SMB:
- SMB 共享可以是 Windows，Linux，或甚至从作为只要它使用 SMB 3.0 或更高版本的设备。 Samba 和 SMB 3.0 的详细信息，请参阅[SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) Samba 实现是否符合 SMB 3.0。
- SMB 共享应具备高可用性。
- 必须将安全性设置在 SMB 共享上正常运行。 下面是共享的从 /etc/samba/smb.conf，示例 SQLData1 所在的名称。

![05-smbsource][1]

## <a name="instructions"></a>Instructions

1. 在 FCI 配置中选择一个将加入的服务器。 并不重要哪一个。
   
1. 获取 mssql 用户有关的信息。
   
   ```bash
    sudo id mssql
   ```
   
   请注意 uid、 gid 和组。 
   
1. 执行 `sudo smbclient -L //NameOrIP/ShareName -U User`。
   
   \<NameOrIP > 是 DNS 名称或托管的 SMB 共享的服务器的 IP 地址。
   
   \<共享名 > 是 SMB 共享的名称。 
   
1. 系统数据库或存储在默认数据位置的任何内容按照以下步骤。 否则请跳到步骤 5。 
   
   1. 请确保 SQL Server 已停止正在努力在服务器上。
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 开关完全是超级用户。 如果成功，将不会收到任何确认。
      
      ```bash
      sudo -i
      ```
      
   1. 要使用 mssql 用户的开关。 如果成功，将不会收到任何确认。
      
      ```bash
      su mssql
      ```
      
   1. 创建一个临时目录来存储 SQL Server 数据和日志文件。 如果成功，将不会收到任何确认。
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir > 是文件夹的名称。 以下示例创建一个名为 /var/opt/mssql/tmp 文件夹。
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. 将 SQL Server 数据和日志文件复制到临时目录。 如果成功，将不会收到任何确认。
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir > 是上一步中的文件夹的名称。
      
   1. 验证文件在目录中。
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir > 是从步骤 d 文件夹的名称。
      
   1. 从现有的 SQL Server 数据目录中删除的文件。 如果成功，将不会收到任何确认。
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. 验证已删除的文件。 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 若要切换回根用户的键入 exit。
      
   1. 装载 SMB 共享的 SQL Server 数据文件夹中。 如果成功，将不会收到任何确认。 此示例演示用于连接到基于 Windows Server 的 SMB 3.0 共享的语法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<服务器名 > 是包含 SMB 共享的服务器名称
      
      \<共享名 > 是共享的名称
      
      \<用户名 > 是要对其进行访问的用户的名称
      
      \<密码 > 用户的密码
      
      \<域 > 是 Active Directory 的名称
      
      \<mssqlUID > 为 mssql 用户的 UID 
      
      \<mssqlGID > 为 mssql 用户 GID
      
   1. 检查以查看装载通过不带任何开关发出装入成功。
      
      ```bash
      mount
      ```
      
   1. 切换到 mssql 用户。 如果成功，将不会收到任何确认。
      
      ```bash
      su mssql
      ```
      
   1. 将文件从临时目录 /var/opt/mssql/data 复制。 如果成功，将不会收到任何确认。
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. 验证文件存在。
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 输入退出以不是 mssql 
      
   1. 输入退出以不是根
   
   1. 启动 SQL Server。 如果已正确复制所有内容和应用的安全设置是否正确，SQL Server 应显示为已启动。
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 若要进一步测试，创建数据库，以确保是完好的权限。 下面的示例使用 Transact-SQL;可以使用 SSMS。
      
      ![10_testcreatedb][2] 
      
   1. 停止 SQL Server，并验证它关闭的情况下。 如果想要添加或测试的其他磁盘，是否不关闭 SQL Server 的添加和测试之前。
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 仅当完成后，卸载共享。 如果没有，完成测试/添加任何附加磁盘后卸载。
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > 是的 IP 地址或 SMB 主机的名称
      
      \<共享名 > 是共享的名称
      
      \<FolderMountedIn > 是在其中安装 SMB 文件夹的名称
      
5. 为系统数据库，例如，用户数据库或备份以外的内容，请执行以下步骤。 如果只使用了默认位置，请跳至步骤 14。
   
   1. 切换到是超级用户。 如果成功，将不会收到任何确认。
      
      ```bash
      sudo -i
      ```
      
   1. 创建 SQL Server 将使用的文件夹。 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<文件夹名 > 是文件夹的名称。 文件夹的完整路径需要指定如果不在正确的位置。 以下示例创建一个名为 /var/opt/mssql/userdata 文件夹。
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. 装载 SMB 共享的 SQL Server 数据文件夹中。 如果成功，将不会收到任何确认。 此示例演示用于连接到基于 Samba 的 SMB 3.0 共享的语法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<服务器名 > 是包含 SMB 共享的服务器名称
      
      \<共享名 > 是共享的名称
      
      \<文件夹名 > 是的最后一步中创建的文件夹名称  
      
      \<用户名 > 是要对其进行访问的用户的名称
      
      \<密码 > 用户的密码
      
      \<mssqlUID > 为 mssql 用户的 UID
      
      \<mssqlGID > 为 mssql 用户 GID。
      
   1. 检查以查看装载通过不带任何开关发出装入成功。
   
   1. 键入 exit 以不再是超级用户。
   
   1. 若要测试，请在该文件夹中创建数据库。 以下示例使用 sqlcmd 创建数据库，将上下文切换到它，验证文件存在于 OS 级别，然后删除该临时位置。 可以使用 SSMS。
   
   1. 卸载共享 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > 是的 IP 地址或 SMB 主机的名称
      
      \<共享名 > 是共享的名称
      
      \<FolderMountedIn > 是在其中安装 SMB 文件夹的名称。
   
1. 重复对其他节点的步骤。

你现已准备好配置 FCI。

## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
