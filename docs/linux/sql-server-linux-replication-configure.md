---
title: 在 Linux 上配置 SQL Server 复制 |Microsoft Docs
description: 本文介绍如何在 Linux 上配置 SQL Server 复制。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 71ad9b87f701a1f1de4f13a7788bba13543056e8
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030014"
---
# <a name="configure-sql-server-replication-on-linux"></a>在 Linux 上配置 SQL Server 复制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 引入了 SQL Server 复制的 Linux 上的 SQL Server 实例。

有关复制的详细信息，请参阅[SQL Server 复制文档](../relational-databases/replication/sql-server-replication.md)。

在 Linux 上使用 SQL Server Management Studio (SSMS) 或 TRANSACT-SQL 存储过程配置复制。

* 若要使用 SSMS，按照这篇文章中的说明。

  在 Windows 操作系统上使用 SSMS 连接到 SQL Server 的实例。 有关背景信息和说明，请参阅[使用 SSMS 管理 Linux 上的 SQL Server](./sql-server-linux-manage-ssms.md)。
  
* 有关使用存储过程示例，请按照[Linux 上的配置 SQL Server 复制](sql-server-linux-replication-tutorial-tsql.md)教程。

## <a name="prerequisites"></a>必要條件

配置发布服务器、 分发服务器和订阅服务器之前, 需要完成 SQL Server 实例的几个配置步骤。

1. 启用 SQL Server 代理以使用复制代理。 所有 Linux 服务器上，在终端中运行以下命令。

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. 配置复制的 SQL Server 实例。 若要配置复制的 SQL Server 实例，请运行`sys.sp_MSrepl_createdatatypemappings`参与复制的所有实例上。

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. 创建快照文件夹。 SQL Server 代理还需要为读/写到快照文件夹。 在分发服务器上创建快照文件夹。

  若要创建快照文件夹，并授予访问权限`mssql`用户，运行以下命令：

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>配置和监视复制使用 SQL Server Management Studio (SSMS)

### <a name="configure-the-distributor"></a>配置分发服务器
  
若要配置分发服务器： 

1. 在 SSMS 连接到的对象资源管理器中的 SQL Server 实例。

1. 右键单击**复制**，然后单击**配置分发...**.

1. 按照上的说明**配置分发向导**。

### <a name="create-publication-and-articles"></a>创建发布和项目

若要创建的发布和文章：

1. 在对象资源管理器，单击**复制** > **本地发布**> **新发布...**.

1. 按指令**新建发布向导**若要配置的类型的复制和属于该发布的文章。

### <a name="configure-the-subscription"></a>配置订阅

若要在对象资源管理器中配置的订阅，请单击**复制** > **本地订阅**> **新订阅...**.

### <a name="monitor-replication-jobs"></a>监视复制作业

使用复制监视器监视复制作业。

在对象资源管理器中右键单击**复制**，然后单击**启动复制监视器**。

## <a name="next-steps"></a>后续步骤

[Linux 上的概念： SQL Server 复制](sql-server-linux-replication.md)

[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
