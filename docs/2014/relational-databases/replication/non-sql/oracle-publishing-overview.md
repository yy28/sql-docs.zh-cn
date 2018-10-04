---
title: Oracle 发布概述 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], Oracle publishing
- snapshot replication [SQL Server], Oracle publishing
- Oracle publishing [SQL Server replication]
- transactional replication, Oracle publishing
- Oracle publishing [SQL Server replication], about Oracle publishing
ms.assetid: 2e013259-0022-4897-a08d-5f8deb880fa8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba97c517967b3a010379e82ee1f230af83c8a490
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214557"
---
# <a name="oracle-publishing-overview"></a>Oracle Publishing Overview
  从 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]开始，可以在复制拓扑中加入 Oracle 发布服务器（自 Oracle 9i 版起）。 可在支持 Oracle 的任何硬件和操作系统上部署发布服务器。 该功能建立在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照复制和事务性复制的坚实基础上，提供了相似的性能和可用性。  
  
 不推荐使用 Oracle 发布。 不推荐异类复制到非 SQL Server 订阅服务器。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="snapshot-replication-for-oracle"></a>Oracle 的快照复制  
 Oracle 快照发布与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快照发布在实现方式上类似。 对 Oracle 发布运行快照代理时，该代理将连接到 Oracle 发布服务器，并处理发布中的每个表。 处理每个表时，代理将检索表行并创建架构脚本，然后将该脚本存储在发布的快照共享中。 每次运行快照代理时都会创建整个数据集，因此在事务复制中出现更改跟踪触发器时，不会将它们添加到 Oracle 表中。 快照复制是迁移数据的一种便利方法，可以将对发布系统的影响降到最低。  
  
## <a name="transactional-replication-for-oracle"></a>Oracle 事务复制  
 Oracle 事务发布是通过使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的事务发布体系结构来实现的；但更改却是通过结合使用 Oracle 数据库上的数据库触发器和日志读取器代理来跟踪的。 Oracle 事务发布的订阅服务器使用快照复制自动进行初始化；在以后发生更改时，将通过日志读取器代理对这些更改进行跟踪，并将更改传递到订阅服务器。  
  
 创建 Oracle 发布时，将为 Oracle 数据库中所有已发布的表创建触发器和跟踪表。 对发布的表进行数据更改时，将激发这些表的数据库触发器，并在复制跟踪表中为修改的每一行插入信息。 然后， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上的日志读取器代理将数据更改信息从跟踪表移动到分发服务器上的分发数据库中。 最后，与在标准事务复制中一样，分发代理将更改从分发服务器移动到订阅服务器。  
  
## <a name="see-also"></a>请参阅  
 [配置 Oracle 发布服务器](configure-an-oracle-publisher.md)   
 [有关 Oracle 发布的术语词汇表](glossary-of-terms-for-oracle-publishing.md)   
 [异类数据库复制](heterogeneous-database-replication.md)  
  
  
