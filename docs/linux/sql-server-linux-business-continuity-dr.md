---
title: "在 Linux 上的 SQL Server 的灾难恢复 |Microsoft 文档"
description: 
author: mihaelab
ms.author: mihaelab
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: c75717c8-c677-4033-8ca6-d0ac93aee04d
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 86f41971e06efb767dde336cf93f9224a204176d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="business-continuity-and-database-recovery-sql-server-on-linux"></a>Linux 上的 SQL Server 的业务连续性和数据恢复

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

组织可以使用 Linux 上的 SQL Server 实现各种各样的服务级协议目标，满足各种业务需求。

这些解决方案超级简单，通过利用虚拟化技术就可实现主机级故障的恢复能力、硬件故障的容错能力，并且高度灵活，使资源得到最大化利用。 这些系统在本地、私有云、公有云或混合环境中均可运行。 灾难恢复和保护最简单的形式是数据库备份。 在 SQL Server 自 2017 年 1 RC2 中可用的简单解决方案包括：

- **VM 故障转移**
    - 针对来宾和 OS 级故障的恢复能力
    - 计划外和计划内事件
    - 最小停机时间修补和升级
    - 以分钟为单位的 RTO


- [**数据库备份和还原**](sql-server-linux-backup-and-restore-database.md) 
    - 针对意外或恶意数据损坏的保护
    - 灾难恢复保护
    - 从几分钟到数小时的 RTO

标准版高可用性和灾难恢复方法可提供与可靠的共享存储基础结构结合使用的实例级保护。 对于 SQL Server 自 2017 年 1 RC2 标准的高可用性包括：

- [**故障转移群集**](sql-server-linux-shared-disk-cluster-configure.md)
    - 实例级保护
    - 自动故障检测和故障转移
    - 针对 OS 和 SQL Server 故障的恢复能力
    - 从几秒到数分钟的 RTO


## <a name="summary"></a>摘要

在 Linux 上的 SQL Server 自 2017 年 1 RC2 包括虚拟化、 备份和还原和故障转移群集，以支持高可用性和灾难恢复。 
