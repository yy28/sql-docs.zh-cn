---
title: “内存中”数据库 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: e4e0e6622a2a313b85dfa00df8c88044486f75f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994995"
---
# <a name="in-memory-database"></a>内存数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

内存数据库是 SQL Server 中利用基于“内存中”的技术的功能的总称。 随着新的基于“内存中”的功能被开发出来，此页面将持续更新。

## <a name="hybrid-buffer-pool"></a>混合缓冲池

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[混合缓冲池](../database-engine/configure-windows/hybrid-buffer-pool.md)允许数据库引擎直接访问存储在持久内存 (PMEM) 设备上的数据库文件中的数据页。

## <a name="memory-optimized-tempdb-metadata"></a>内存优化 TempDB 元数据

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了一个新功能，即[内存优化 tempdb 元数据](./databases/tempdb-database.md#memory-optimized-tempdb-metadata)，它有效地消除了某些争用瓶颈，并为 tempdb 繁重的工作负载解锁了新级别的可伸缩性。

## <a name="in-memory-oltp"></a>内存中 OLTP

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[内存中 OLTP](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) 是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 中用于优化事务处理、数据引入、数据加载和瞬态数据方案性能的核心技术。

适用于：[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  。

## <a name="persistent-memory-support-for-linux"></a>对 Linux 的持久内存支持

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 向 Linux 添加了对持久内存 (PMEM) 设备的支持，提供了对放置在[持久内存](../linux/sql-server-linux-configure-pmem.md)上的数据和事务日志文件的完整启用。

适用于：[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  。
