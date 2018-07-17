---
title: 复制类型 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db941e69711c51a6799c1b94723ce90c64c96e6a
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350949"
---
# <a name="types-of-replication"></a>复制类型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供以下类型的复制以用于分布式应用程序：  
  
-   事务复制。 有关详细信息，请参阅[事务复制](../../relational-databases/replication/transactional/transactional-replication.md)。  
  
-   合并复制。 有关详细信息，请参阅[合并复制](../../relational-databases/replication/merge/merge-replication.md)。  
  
-   快照复制。 有关详细信息，请参阅[快照复制](../../relational-databases/replication/snapshot-replication.md)。  
  
 为应用程序选择的复制类型取决于多种因素，其中包括实际复制环境、要复制的数据类型和数量，以及是否在订阅服务器上更新数据等等。 实际环境包括复制中所涉及的计算机数量和位置，以及这些计算机是客户端（工作站、便携式电脑或手持设备）还是服务器。  
  
 每种复制类型通常都开始于发布服务器和订阅服务器之间的已发布对象的初始同步。 此初始同步可以由带有“快照” 的复制执行，该快照为发布所指定的所有对象和数据的副本。 快照在创建之后，便被传递到订阅服务器。 对于某些应用程序而言，只需快照复制即可。 对于另一些类型的应用程序而言，后续数据更改应随着时间而增量式地传递到订阅服务器，这一点很重要。 某些应用程序也需要更改从订阅服务器传递回发布服务器。 事务复制和合并复制为这些类型的应用程序提供了若干选项。  
  
 不会跟踪快照复制的数据更改；每次应用快照时，都将完全覆盖现有数据。 事务复制通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务日志跟踪更改，而合并复制则通过触发器和元数据表跟踪更改。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理概述](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
