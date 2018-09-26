---
title: 在 Linux 上配置快照文件夹共享 SQL Server 复制 |Microsoft Docs
description: 本文介绍如何在 Linux 上配置快照文件夹共享 SQL Server 复制。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 9/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6dd5887f4db97ae4d8f52103fd29403e7eb4c51e
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715061"
---
# <a name="configure-replication-with-non-default-ports"></a>使用非默认端口配置复制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在配置了 network.tcpport mssql-conf 设置任何端口上侦听的 Linux 实例上，可以使用 SQL Server 配置复制。 端口需要追加到的服务器名称在配置期间如果满足以下条件：

1. 复制设置涉及到 Linux 上的 SQL Server 实例
2. （Windows 或 Linux） 的任何实例正在侦听非默认端口。 

实例的服务器名称可通过运行 @@servername实例上。

## <a name="examples"></a>示例

Server1 在 Linux 上的端口 1500年上进行侦听。 若要配置分发 Server1，运行`sp_adddistributor`与`@distributor`。 例如： 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

Server1 在 Linux 上的端口 1500年上进行侦听。 若要配置分发服务器的发布服务器，请运行`sp_adddistpublisher`与`@publisher`。 例如：

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

Server2 在 Linux 上的端口 6549 上侦听。 若要将 Server2' 配置为订阅服务器，运行`sp_addsubscription`与`@subscriber`。 例如：

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

Server3 在端口上侦听 6549 在 Windows 上使用 Server3 的服务器名称和实例名称来 MSSQL2017。 若要将 Server3' 配置为订阅服务器，运行`sp_addsubscription`与`@subscriber`。 例如：

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>后续步骤

[Linux 上的概念： SQL Server 复制](sql-server-linux-replication.md)

[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

