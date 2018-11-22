---
title: 混合缓冲池 | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.openlocfilehash: a8098c38b72ba44ab973fe5564b93740252bafc6
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560304"
---
# <a name="hybrid-buffer-pool"></a>混合缓冲池
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在 SQL Server 2019 CTP 2.1 中，SQL Server 数据库引擎引入了一项新功能，通过该功能可以直接访问存储在持久内存 (PMEM) 设备中的数据库文件中的数据页。 

在没有持久内存的传统系统中，SQL Server 将数据页缓存在缓冲池中。 使用混合缓冲池，SQL Server 会跳过将页面副本执行到缓冲池的基于 DRAM 的部分，直接在 PMEM 设备上的数据库文件上引用该页面。 可使用内存映射 I/O（也称为 enlightenment）访问混合缓冲池 PMEM 中的数据文件。

PMEM 设备只能直接引用干净页。 页面变脏以后会保存在 DRAM 中，并最终写回到 PMEM 设备。

Windows 和 Linux 上都提供了此功能。

## <a name="enable-hybrid-buffer-pool"></a>启用混合缓冲池

在 CTP 2.1 上必须启用启动跟踪标志 809 才能使用混合缓冲池。

## <a name="best-practices-for-hybrid-buffer-pool"></a>混合缓冲池的最佳做法

* 在 Windows 上格式化 PMEM 设备时，使用可用于 NTFS 的最大分配单元大小（Windows Server 2019 中为 2MB）并确保已为 DAX (DirectAccess) 启用该设备
  