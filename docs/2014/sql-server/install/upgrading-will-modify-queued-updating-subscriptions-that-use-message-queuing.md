---
title: 升级将修改使用消息队列的排队更新订阅 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 76af35f994413ad1e02bcafaaa8499e42fe232c7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62990147"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>升级将修改使用消息队列的排队更新订阅
  升级顾问检测到您可能有一个或多个使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 消息队列（又称为 MSMQ）的排队更新订阅。 复制不再支持消息队列；因此，将对订阅进行修改以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列。  
  
 值**sql**允许。 在升级期间，将修改使用消息队列的现有发布从而可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列。 如果某些应用程序依赖于使用消息队列的排队更新，将必须重写这些应用程序以适应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列。 有关排队更新订阅的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“事务复制的可更新订阅”。  
  
 如果在升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时消息队列服务处于运行之中，则升级过程将删除现有的消息队列订阅队列。  
  
 如果未运行消息队列服务，请在升级完成后手动删除这些队列。 有关如何删除队列的详细信息，请参阅 Windows 文档。  
  
## <a name="see-also"></a>请参阅  
 [复制升级问题](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
