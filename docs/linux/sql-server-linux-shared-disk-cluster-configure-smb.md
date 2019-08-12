---
title: 配置故障转移群集实例存储 SMB - Linux 上的 SQL Server
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e93b7fac2f75758a0a95a4053ee0a989e410c70e
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032322"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>配置故障转移群集实例 - SMB - Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上为故障转移群集实例 (FCI) 配置 SMB 存储。 
 
在非 Windows 环境中，SMB 通常称为通用 Internet 文件系统 (CIFS) 共享，并通过 Samba 实现。 在 Windows 环境中，通过以下方式访问 SMB 共享：\\SERVERNAME\SHARENAME。 对于基于 Linux 的 SQL Server 安装，必须将 SMB 共享装载为文件夹。

## <a name="important-source-and-server-information"></a>重要的源和服务器信息

下面是成功使用 SMB 的一些提示和说明：
- SMB 共享可位于 Windows、Linux 甚至设备（只要它使用的是 SMB 3.0 或更高版本）上。 有关 Samba 和 SMB 3.0 的详细信息，请参阅 [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0)，了解你的 Samba 实现是否符合 SMB 3.0。
- SMB 共享应高度可用。
- 必须在 SMB 共享上正确设置安全性。 下面是 /etc/samba/smb.conf 中的一个示例，其中 SQLData1 是共享的名称。

![05-smbsource][1]

## <a name="instructions"></a>Instructions

1. 选择将参与 FCI 配置的其中一个服务器。 选哪一个都没有关系。
   
1. 获取有关 mssql 用户的信息。
   
   ```bash
    sudo id mssql
   ```
   
   请注意 UID、GID 和组。 
   
1. 执行 `sudo smbclient -L //NameOrIP/ShareName -U User`。
   
   \<NameOrIP> 是托管 SMB 共享的服务器的 DNS 名称或 IP 地址。
   
   \<ShareName> 是 SMB 共享的名称。 
   
1. 对于系统数据库或存储在默认数据位置的任何内容，请执行以下步骤。 否则，请跳至步骤 5。 
   
   1. 确保在正在使用的服务器上停止 SQL Server。
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 完全切换为超级用户。 如果成功，则不会收到任何确认。
      
      ```bash
      sudo -i
      ```
      
   1. 切换为 mssql 用户。 如果成功，则不会收到任何确认。
      
      ```bash
      su mssql
      ```
      
   1. 创建一个临时目录来存储 SQL Server 数据和日志文件。 如果成功，则不会收到任何确认。
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir> 是文件夹名称。 以下示例会创建名为 /var/opt/mssql/tmp 的文件夹。
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. 将 SQL Server 数据和日志文件复制到临时目录。 如果成功，则不会收到任何确认。
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir> 是上一步中的文件夹的名称。
      
   1. 验证文件是否位于目录中。
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir> 是步骤 d 中文件夹的名称。
      
   1. 删除现有 SQL Server 数据目录中的文件。 如果成功，则不会收到任何确认。
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. 验证文件是否已删除。 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 键入 exit 切换回根用户。
      
   1. 将 SMB 共享装载到 SQL Server 数据文件夹中。 如果成功，则不会收到任何确认。 此示例展示了连接到基于 Windows Server 的 SMB 3.0 共享所用的语法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> 是具有 SMB 共享的服务器的名称
      
      \<ShareName> 是共享的名称
      
      \<UserName> 是访问共享的用户的名称
      
      \<Password> 是用户的密码
      
      \<domain> 是 Active Directory 的名称
      
      \<mssqlUID> 是 mssql 用户的 UID 
      
      \<mssqlGID> 是 mssql 用户的 GID
      
   1. 通过发出不带开关的 mount 来检查装载是否成功。
      
      ```bash
      mount
      ```
      
   1. 切换为 mssql 用户。 如果成功，则不会收到任何确认。
      
      ```bash
      su mssql
      ```
      
   1. 从临时目录 /var/opt/mssql/data 复制文件。 如果成功，则不会收到任何确认。
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. 验证文件是否存在。
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 输入 exit 以不再是 mssql 用户 
      
   1. 输入 exit 以不再是根用户
   
   1. 启动 SQL Server。 如果正确复制了所有内容并正确应用了安全性，则 SQL Server 应显示为已启动。
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 若要进一步测试，请创建一个数据库来确保权限是正常的。 下面的示例使用 Transact-SQL；你可以使用 SSMS。
      
      ![10_testcreatedb][2] 
      
   1. 停止 SQL Server 并验证它是否已关闭。 如果要添加或测试其他磁盘，在添加和测试这些磁盘之前，请不要关闭 SQL Server。
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 仅在完成后才卸载共享。 如果未完成，请在完成任何其他磁盘的测试/添加操作后再卸载。
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> 是 SMB 主机的 IP 地址或名称
      
      \<ShareName> 是共享的名称
      
      \<FolderMountedIn> 是装载 SMB 的文件夹的名称
      
5. 对于系统数据库以外的其他内容，例如用户数据库或备份，请按照以下步骤操作。 如果仅使用默认位置，请跳至步骤 14。
   
   1. 切换为超级用户。 如果成功，则不会收到任何确认。
      
      ```bash
      sudo -i
      ```
      
   1. 创建将由 SQL Server 使用的文件夹。 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<FolderName> 是文件夹名称。 如果不在正确的位置，则需要指定文件夹的完整路径。 以下示例将创建名为 /var/opt/mssql/userdata 的文件夹。
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. 将 SMB 共享装载到 SQL Server 数据文件夹中。 如果成功，则不会收到任何确认。 此示例展示了连接到基于 Samba 的 SMB 3.0 共享所用的语法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> 是具有 SMB 共享的服务器的名称
      
      \<ShareName> 是共享的名称
      
      \<FolderName> 是在上一步中创建的文件夹的名称  
      
      \<UserName> 是访问共享的用户的名称
      
      \<Password> 是用户的密码
      
      \<mssqlUID> 是 mssql 用户的 UID
      
      \<mssqlGID> 是 mssql 用户的 GID。
      
   1. 通过发出不带开关的 mount 来检查装载是否成功。
   
   1. 键入 exit 以不再是超级用户。
   
   1. 若要进行测试，请在该文件夹中创建数据库。 以下示例使用 sqlcmd 创建数据库，将上下文切换到该数据库，验证操作系统级别是否存在文件，然后删除临时位置。 你可以使用 SSMS。
   
   1. 卸载共享 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> 是 SMB 主机的 IP 地址或名称
      
      \<ShareName> 是共享的名称
      
      \<FolderMountedIn> 是装载 SMB 的文件夹的名称。
   
1. 对其他节点重复这些步骤。

现在可以配置 FCI 了。

## <a name="next-steps"></a>后续步骤

[配置故障转移群集实例 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
