---
title: Linux 上的 SQL Server 复制
description: 本文介绍 Linux 上的 SQL Server 复制。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b049866d9752485cb1b9eb609404a3bd86f28a41
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065193"
---
# <a name="sql-server-replication-on-linux"></a>Linux 上的 SQL Server 复制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 介绍 Linux 上的 SQL Server 实例的 SQL Server 复制。

使用 SQL Server Management Studio (SSMS) [复制存储过程](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)配置 Linux 上的复制。

SQL Server 实例可以参与任何复制角色：

* 发布服务器
* 分发服务器
* 订阅服务器

复制架构可以混合和匹配操作系统平台。 例如，复制架构可能包括发布服务器和分发服务器的 Linux 上的 SQL Server 实例，并且订阅服务器包含 Windows 和 Linux 上的 SQL Server 实例。

Linux 上的 SQL Server 实例可以参与任何类型的复制。

* 事务性
* 合并
* 快照

有关复制的详细信息，请参阅 [SQL Server 复制文档](../relational-databases/replication/sql-server-replication.md)。

## <a name="supported-features"></a>支持的功能

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 支持以下复制功能：

* 快照复制
* 事务复制
* 合并复制
* 对等复制
* 使用非默认端口的复制 <!--Add link to explanation-->
* 使用 AD 身份验证的复制
* 跨 Windows 和 Linux 的复制配置
* 事务复制的及时更新

## <a name="limitations"></a>限制

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 不支持以下功能：

* 即时更新订阅者
* Oracle 发布

## <a name="next-steps"></a>后续步骤

[配置 Linux 上的 SQL Server 复制](sql-server-linux-replication-tutorial-tsql.md)

[示例：配置 Linux 上的 SQL Server 复制](sql-server-linux-replication-configure.md)
