---
title: 检查磁盘输入和输出子系统是否存在 IO 延迟问题 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5cdcc410cc83d7f7fa53d937f6011ad2624655fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157335"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>检查磁盘输入和输出子系统是否存在 IO 延迟问题
  此规则检查计算机事件日志中是否存在错误消息 833。 该消息指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已从磁盘发出读取或写入请求，并且表明该请求返回所用的时间已超过 15 秒。 此错误由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 报告，表示磁盘 I/O 子系统有问题。 延迟此长度的时间可能会严重损坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境的性能。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 通过检查系统事件日志获得硬件相关错误消息来纠正引错误。 并且，如果有特定于硬件的日志，也要进行检查。  
  
 使用性能监视器检查以下计数器：  
  
-   Average Disk Sec/Transfer  
  
-   Average Disk Queue Length  
  
-   Current Disk Queue Length  
  
 例如，运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的 Average Disk Sec/Transfer 时间通常少于 15 毫秒。 如果 Average Disk Sec/Transfer 值增加，则表示磁盘 I/O 子系统未能完全满足 I/O 需求。  
  
## <a name="for-more-information"></a>有关详细信息  
 [MSSQLSERVER_833](../errors-events/mssqlserver-833-database-engine-error.md)  
  
 [Microsoft 知识库文章 897284](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [SQL Server I/O Basics, Chapter 2（SQL Server I/O 基础知识第 2 章）](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
