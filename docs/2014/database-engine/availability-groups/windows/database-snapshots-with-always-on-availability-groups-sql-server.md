---
title: 数据库快照与 AlwaysOn 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cba02aa87e800391ffba3c791c1ee4341462c3f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814653"
---
# <a name="database-snapshots-with-alwayson-availability-groups-sql-server"></a>含有 AlwaysOn 可用性组的数据库快照 (SQL Server)
  您可在可用性组中的主数据库或辅助数据库上创建数据库快照。 副本角色必须是 PRIMARY 或 SECONDARY，且不处于 RESOLVING 状态。  
  
 当您创建一个数据库快照时，我们建议数据库同步状态是 SYNCHRONIZING 或 SYNCHRONIZED。 但是，当数据库同步状态为 NOT SYNCHRONIZING 时，可以创建数据库快照。  
  
 如果辅助副本断开与主副本的连接，则该辅助副本上的数据库快照应该继续工作。  
  
 某些 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 情况会导致源数据库及其数据库快照重新启动，暂时断开用户连接。 这些情况如下所示：  
  
-   主副本更改角色，无论是因为当前主副本脱机并且在同一服务器实例上恢复联机状态，还是因为可用性组故障转移。  
  
-   数据库进入辅助角色。  
  
 如果承载数据库快照的可用性副本故障转移，则该数据库快照将保留在创建了这些快照的服务器实例上。 用户可以在故障转移后继续使用快照。如果性能是您的环境中的关注点，我们建议您仅在配置为手动故障转移模式的辅助副本承载的辅助数据库上创建数据库快照。  如果您曾经将可用性组手动故障转移到此辅助副本，则可以在其他辅助副本上创建一组新的数据库快照，将客户端重定向到这些新的数据库快照，并且从新的主数据库上删除所有数据库快照。  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [数据库快照 (SQL Server)](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
