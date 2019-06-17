---
title: 事务升级 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf30b06849c0384d118edf635a6361712c2d22f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874761"
---
# <a name="transaction-promotion"></a>事务升级
  事务*促销*介绍可以进行自动提升为完全可分发事务根据需要轻型本地事务。 当在服务器上的数据库事务内调用托管存储过程时，会在本地事务的上下文中运行公共语言运行时 (CLR) 代码。  如果在数据库事务内打开到远程服务器的连接，则到远程服务器的连接会登记在分布式事务中，并且本地事务会自动升级为分布式事务。 因此，通过将分布式事务的创建延迟到需要创建时才进行，事务升级可以将分布式事务的开销降至最低。 如果已使用 `Enlist` 关键字启用了事务升级，则事务升级将自动进行，而不需要开发人员干预。 用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 .NET Framework 数据提供程序可为事务升级提供支持，这是通过 .NET Framework `System.Data.SqlClient` 命名空间中的类处理的。  
  
## <a name="the-enlist-keyword"></a>Enlist 关键字  
 `ConnectionString` 对象的 `SqlConnection` 属性支持 `Enlist` 关键字，该关键字指示 `System.Data.SqlClient` 是否检测事务上下文并在分布式事务中自动登记连接。 如果此关键字设置为 True（默认设置），则会在打开的线程的当前事务上下文中自动登记连接。 如果此关键字设置为 False，则 SqlClient 连接不会与分布式事务交互。 如果未在连接字符串中指定 `Enlist`，并且如果在打开相应连接时检测到一个分布式事务，则会在此分布式事务中自动登记此连接。  
  
## <a name="distributed-transactions"></a>分布式事务  
 分布式事务通常会使用大量的系统资源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 会管理此类事务，并集成在这些事务中访问的所有资源管理器。 另一方面，事务升级是有效地将工作委托给简单 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务的 `System.Transactions` 事务的特殊形式。 `System.Transactions`、`System.Data.SqlClient` 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会对处理事务时涉及到的工作进行协调，并按照需要将其升级为完全分布式事务。  
  
 使用事务升级的优点在于：在打开一个具有活动 `TransactionScope` 事务的连接而未打开任何其他连接的情况下，该事务会以轻型事务的形式提交，而不是产生完全分布式事务的额外开销。 有关详细信息`TransactionScope`，请参阅[使用 System.Transactions](../native-client-ole-db-transactions/transactions.md)。  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成和事务](clr-integration-and-transactions.md)  
  
  
