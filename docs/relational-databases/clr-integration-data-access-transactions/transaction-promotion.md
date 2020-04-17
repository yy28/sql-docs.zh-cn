---
title: 交易促销 |微软文档
description: 在 SQL Server CLR 集成中，可以通过事务升级将轻量级本地事务提升为完全可分配事务。
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487462"
---
# <a name="transaction-promotion"></a>事务升级
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  事务*升级*描述一个轻量级的本地事务，可以根据需要自动提升为完全可分配事务。 当在服务器上的数据库事务内调用托管存储过程时，会在本地事务的上下文中运行公共语言运行时 (CLR) 代码。  如果在数据库事务内打开到远程服务器的连接，则到远程服务器的连接会登记在分布式事务中，并且本地事务会自动升级为分布式事务。 因此，通过将分布式事务的创建延迟到需要创建时才进行，事务升级可以将分布式事务的开销降至最低。 事务升级是自动的，如果已使用**Enlist**关键字启用，并且不需要开发人员的干预。 .NET 框架数据提供程序用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持事务升级，通过 .NET 框架**系统中的**类进行处理。  
  
## <a name="the-enlist-keyword"></a>登记关键字  
 **SqlConnection**对象的**ConnectString**属性支持**Enlist**关键字，该关键字指示**System.Data.SqlClient**是否检测事务上下文并自动在分布式事务中登记连接。 如果此关键字设置为 True（默认设置），则会在打开的线程的当前事务上下文中自动登记连接。 如果此关键字设置为 False，则 SqlClient 连接不会与分布式事务交互。 如果在连接字符串中未指定**Enlist，** 则如果在打开连接时检测到连接，则连接将自动登记在分布式事务中。  
  
## <a name="distributed-transactions"></a>分布式事务  
 分布式事务通常会使用大量的系统资源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 会管理此类事务，并集成在这些事务中访问的所有资源管理器。 另一方面，事务促进是一种特殊形式的**系统。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **系统.事务**，**系统.Data.SqlClient，** 并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]协调处理事务所涉及的工作，根据需要将其提升为完全分布式事务。  
  
 使用事务升级的好处是，当与活动**事务范围**事务打开连接，并且未打开任何其他连接时，事务将作为轻量级事务提交，而不是产生完全分布式事务的额外开销。 有关**事务范围**的详细信息，请参阅[使用系统。](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成和事务](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
