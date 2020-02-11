---
title: 数据库镜像不支持跨数据库事务或 AlwaysOn 可用性组（SQL Server） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c3616e40ff54c67d27902ddf9454084fb62e282
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813652"
---
# <a name="cross-database-transactions-not-supported-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>数据库镜像或 AlwaysOn 可用性组不支持跨数据库事务 (SQL Server)
  
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]或数据库镜像不支持跨数据库事务和分布式事务。 这是因为以下原因无法保证事务的原子性/完整性：  
  
-   对于跨数据库事务：每个数据库独立提交。 因此，即使对于单个可用性组中的数据库，在一个数据库提交事务后、但是在另一个数据库提交前可能发生故障转移。 对于数据库镜像，此问题很复杂，因为在故障转移后，镜像数据库所在的服务器实例通常不同于其他数据库的服务器实例，即使在两个相同伙伴之间对两个数据库进行镜像，也无法保证两个数据库同时进行故障转移。  
  
-   对于分布式事务：故障转移后，新主体服务器/主副本无法连接到前一个主体服务器/主副本的分布式事务处理协调器。 因此，新主体服务器/主副本无法获取事务状态。  
  
 以下数据库镜像示例说明了如何可能出现逻辑上的不一致。 在此示例中，应用程序使用跨数据库事务插入两行数据：将其中一行插入镜像数据库 A 中的表，将另一行插入另一个数据库 B 中的表。数据库 A 在具有自动故障转移功能的高安全性模式下进行镜像。 提交事务时，数据库 A 不可用，镜像会话将故障自动转移到数据库 A 的镜像数据库。  
  
 故障转移之后，跨数据库事务可能会在数据库 B 上成功提交，但不可能会在故障转移的数据库中成功提交。 如果在发生故障之前，数据库 A 的原始主体服务器未能将跨数据库事务的日志发送到镜像服务器，则可能会出现这种情况。 故障转移之后，该事务将不存在于新的主体服务器上。 数据库 A 和数据库 B 出现不一致，因为在数据库 B 中插入的数据保持完好无损，而在数据库 A 中插入的数据已经丢失。  
  
 使用 MS DTC 事务时可能会出现类似的情况。 例如，故障转移后，新主体将访问 MS DTC。 但是 MS DTC 不能识别新的主体服务器，因而会终止被认为已在其他数据库中提交了的、所有“准备提交”的事务。  
  
> [!IMPORTANT]  
>  将数据库镜像或可用性组与 DTC 搭配使用不会导致 SQL Server 安装失去支持。 但是，如果数据库为数据库镜像会话或可用性组的一部分，且在数据库中使用了 DTC，则仅当支持问题与将数据库镜像或可用性组与 DTC 搭配使用无关时将由 Microsoft 组织调查。  
  
  
