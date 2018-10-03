---
title: Linux 上的 SQL Server 复制 |Microsoft Docs
description: 本文介绍在 Linux 上的 SQL Server 复制。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6c4bad8947944d59208a0516e5950d36f64a84e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734125"
---
# <a name="sql-server-replication-on-linux"></a>Linux 上的 SQL Server 复制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 引入了 SQL Server 复制的 Linux 上的 SQL Server 实例。

使用 SQL Server Management Studio (SSMS) 在 Linux 上配置复制[复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

SQL Server 的实例可以参与任何复制角色：

* 发布服务器
* 分发服务器
* 订阅服务器

复制架构可以混合和匹配操作系统平台。 例如，复制架构可以使用 SQL Server 的实例在 Linux 上的发布服务器和分发服务器上，而订阅服务器可以包含的 Windows 上的 SQL Server 实例。

Linux 上的 SQL Server 实例可以参与任何类型的复制。

* 事务性
* 合并
* 快照

有关复制的详细信息，请参阅[SQL Server 复制文档](../relational-databases/replication/sql-server-replication.md)。

## <a name="supported-features"></a>支持的功能

有关[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]支持以下复制功能：

* 快照复制
* 事务复制
* 合并复制
* 对等复制
* 复制具有非默认端口 <!--Add link to explanation-->
* 复制通过 AD 身份验证
* 在 Windows 和 Linux 上的复制配置
* 对于事务复制的立即更新

## <a name="limitations"></a>限制

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 不支持以下功能：

* 立即更新订阅服务器

## <a name="next-steps"></a>后续步骤

[在 Linux 上配置 SQL Server 复制](sql-server-linux-replication-tutorial-tsql.md)

[示例： 在 Linux 上配置 SQL Server 复制](sql-server-linux-replication-configure.md)
