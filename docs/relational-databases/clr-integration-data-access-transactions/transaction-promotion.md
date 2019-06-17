---
title: 事务升级 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 893068965ab4566b6f6e4f78e39141de9be2b6ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63044291"
---
# <a name="transaction-promotion"></a>事务升级
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  事务*促销*介绍可以进行自动提升为完全可分发事务根据需要轻型本地事务。 当在服务器上的数据库事务内调用托管存储过程时，会在本地事务的上下文中运行公共语言运行时 (CLR) 代码。  如果在数据库事务内打开到远程服务器的连接，则到远程服务器的连接会登记在分布式事务中，并且本地事务会自动升级为分布式事务。 因此，通过将分布式事务的创建延迟到需要创建时才进行，事务升级可以将分布式事务的开销降至最低。 事务升级是自动的如果已启用使用**登记**关键字，并且不需要开发人员参与。 用于.NET Framework 数据提供程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持事务升级，通过.NET Framework 中的类来处理**System.Data.SqlClient**命名空间。  
  
## <a name="the-enlist-keyword"></a>Enlist 关键字  
 **ConnectionString**的属性**SqlConnection**对象支持**登记**关键字，指示是否**System.Data.SqlClient**检测事务上下文并自动登记分布式事务中的连接。 如果此关键字设置为 True（默认设置），则会在打开的线程的当前事务上下文中自动登记连接。 如果此关键字设置为 False，则 SqlClient 连接不会与分布式事务交互。 如果**登记**未在连接自动登记在分布式事务中，如果在打开连接时检测到一个连接字符串中指定。  
  
## <a name="distributed-transactions"></a>分布式事务  
 分布式事务通常会使用大量的系统资源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 会管理此类事务，并集成在这些事务中访问的所有资源管理器。 事务升级后，就是一种特殊形式**System.Transactions**有效地将工作委托给一个简单的事务[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]事务。 **System.Transactions**， **System.Data.SqlClient**，和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]协调在处理事务，将其提升为完全分布式事务中，根据所涉及的工作。  
  
 使用事务升级的好处是，当打开连接时处于活动状态**TransactionScope**事务和任何其他连接处于打开状态，作为轻型事务的事务提交而非不会产生完全分布式事务的额外开销。 有关详细信息**TransactionScope**，请参阅[使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)。  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成和事务](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
