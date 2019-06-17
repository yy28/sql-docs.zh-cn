---
title: 在 Linux 上配置快照文件夹共享 SQL Server 复制 |Microsoft Docs
description: 本文介绍如何在 Linux 上配置快照文件夹共享 SQL Server 复制。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7569eaf92484038e998595405df42dd1f2d31b3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718163"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>使用共享配置复制快照文件夹

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

快照文件夹是已为共享; 指定的目录代理的读取和写入到此文件夹必须具有足够权限来访问它。

![复制关系图][1]

### <a name="replication-snapshot-folder-share-explained"></a>复制快照文件夹共享所述

之前示例中，让我们通过 SQL Server 复制中使用 samba 共享的方式。 下面是此工作原理的基本示例。

1. Samba 共享配置，文件中写入到`/local/path1`复制的发布服务器上的代理可以看到由订阅服务器
2. SQL Server 配置为使用共享路径，设置发布服务器上，在分发服务器，这样就可以查看所有实例时 `//share/path`
3. SQL Server 将查找从的本地路径`//share/path`以了解在何处查找文件
4. SQL Server 读取/写入到由 samba 共享提供支持的本地路径


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>配置快照文件夹的 samba 共享 

复制代理需要能够访问其他计算机上的快照文件夹的复制主机之间共享的目录。 例如，在事务请求复制分发代理位于订阅服务器上，需要访问分发服务器，以获取文章。 在本部分中，我们将逐一介绍如何在两个复制主机上配置 samba 共享的示例。


## <a name="steps"></a>步骤

例如，我们将主机 1 与主机 2 （订阅服务器） 使用 Samba 共享 （分发服务器） 上配置的快照文件夹。 

### <a name="install-and-start-samba-on-both-machines"></a>安装并启动两台计算机上的 Samba 

在 Ubuntu 上：

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

在 RHEL:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>在主机 1 上 （分发服务器） 安装 Samba 共享 

1. 设置用户和 samba 的密码：

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. 编辑`/etc/samba/smb.conf`包括以下条目，并填写*share_name*并*路径*字段
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **示例**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>在主机 2 （订阅服务器） 上装载 Samba 共享

编辑该命令，使用正确的路径和 machine2 上运行以下命令：

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **示例**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>在两个主机配置上的 SQL Server Linux 实例以使用快照共享

添加下面的章节`mssql.conf`两台计算机上。 任何位置使用，/ 共享/路径的 samba 共享。 在此示例中，它将是 `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **示例**

  在 host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  在 host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>配置发布服务器使用共享的路径

* 设置复制时, 使用的共享路径 （例如 `//host1/mssql_data`
* 地图`//host1/mssql_data`到本地目录并添加到映射`mssql.conf`。

## <a name="next-steps"></a>后续步骤

[概念：Linux 上的 SQL Server 复制](sql-server-linux-replication.md)

[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
