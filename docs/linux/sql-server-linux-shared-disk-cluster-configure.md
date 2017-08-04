---
title: "为在 Linux 上的 SQL Server 配置共享的磁盘群集 |Microsoft 文档"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92b4cb2500d4fd8a1643488593c40e97b1ff6454
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---

# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Linux 上的 SQL Server 的共享磁盘群集

可以通过 Linux 配置共享存储的高可用性群集，以允许 SQL Server 实例从一个节点故障转移到另一个节点。 在典型群集中，两个或多个服务器均连接到共享存储。 服务器是群集节点。 故障转移群集提供实例级保护，通过允许 SQL Server 在两个或更多节点之间进行故障转移来缩短恢复时间。 配置步骤取决于 Linux 分发版和群集解决方案。 下表标识了经过验证的群集解决方案的具体步骤。  

|Distribution |主题 
|----- |-----
|**Red Hat Enterprise Linux 与 HA 外接程序** |[配置](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[操作](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server HA 外接程序与** |[配置](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>后续步骤


