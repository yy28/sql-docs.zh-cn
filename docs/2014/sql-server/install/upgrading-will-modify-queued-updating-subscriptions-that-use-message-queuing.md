---
title: 升级将修改使用消息队列的排队更新订阅 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: efb1b244385061bee985ec04b5f90d3fb349aef3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016737"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>升级将修改使用消息队列的排队更新订阅
  升级顾问检测到您可能有一个或多个使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 消息队列（又称为 MSMQ）的排队更新订阅。 复制不再支持消息队列；因此，将对订阅进行修改以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列。  
  
 只有值**sql**允许。 在升级期间，将修改使用消息队列的现有发布从而可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列。 如果某些应用程序依赖于使用消息队列的排队更新，将必须重写这些应用程序以适应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 队列。 有关排队更新订阅的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“事务复制的可更新订阅”。  
  
 如果在升级 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时消息队列服务处于运行之中，则升级过程将删除现有的消息队列订阅队列。  
  
 如果未运行消息队列服务，请在升级完成后手动删除这些队列。 有关如何删除队列的详细信息，请参阅 Windows 文档。  
  
## <a name="see-also"></a>请参阅  
 [复制升级问题](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  