---
title: 事务升级 |Microsoft Docs
description: 在 SQL Server CLR 集成中，可以通过事务升级将轻型本地事务提升为完全可分发的事务。
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
ms.openlocfilehash: e77409f6bf6c71363e030f29f86f41205dd4a0f0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487462"
---
# <a name="transaction-promotion"></a>事务升级
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  事务*升级*描述了可根据需要自动提升为完全可分发事务的轻型本地事务。 当在服务器上的数据库事务内调用托管存储过程时，会在本地事务的上下文中运行公共语言运行时 (CLR) 代码。  如果在数据库事务内打开到远程服务器的连接，则到远程服务器的连接会登记在分布式事务中，并且本地事务会自动升级为分布式事务。 因此，通过将分布式事务的创建延迟到需要创建时才进行，事务升级可以将分布式事务的开销降至最低。 如果事务升级是使用**征用**关键字启用的，并且不需要开发人员干预，则事务升级是自动进行的。 的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .NET Framework 数据提供程序提供对事务提升的支持，该支持通过 .NET Framework **SqlClient**命名空间中的类进行处理。  
  
## <a name="the-enlist-keyword"></a>征用关键字  
 **SqlConnection**对象的**ConnectionString**属性支持**征用**关键字，该关键字指示**SqlClient**是否检测事务上下文并自动在分布式事务中登记连接。 如果此关键字设置为 True（默认设置），则会在打开的线程的当前事务上下文中自动登记连接。 如果此关键字设置为 False，则 SqlClient 连接不会与分布式事务交互。 如果未在连接字符串中指定**登记**，则连接将在连接打开时被检测到的分布式事务中自动登记。  
  
## <a name="distributed-transactions"></a>分布式事务  
 分布式事务通常会使用大量的系统资源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 会管理此类事务，并集成在这些事务中访问的所有资源管理器。 另一方面，事务升级是一种特殊形式的**系统**事务事务，它可以有效地将工作委托给简单[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的事务。 **SqlClient** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **和协调**处理事务时涉及到的工作，根据需要将其提升为完整的分布式事务。  
  
 使用事务升级的好处是，在使用活动的**TransactionScope**事务打开连接并且未打开任何其他连接时，事务作为轻型事务提交，而不是产生完全分布式事务的额外开销。 有关**TransactionScope**的详细信息，请参阅[使用 system.object](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成和事务](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
