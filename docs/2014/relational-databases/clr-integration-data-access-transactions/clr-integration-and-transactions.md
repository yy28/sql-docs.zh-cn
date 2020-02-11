---
title: CLR 集成和事务 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c6d1b302d6ed0f35ce6fcb60e0afb90415c21d1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874818"
---
# <a name="clr-integration-and-transactions"></a>CLR 集成和事务
  
  `System.Transactions` 命名空间提供与 ADO.NET 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成完全集成的新事务框架。 
  `System.Transactions` 与 ADO.NET 配合工作，以扩展和简化托管应用程序中本地事务和分布式事务的使用。  
  
> [!NOTE]  
>  CLR 用户定义过程 (UDP) 不能与运行此过程的同一服务器建立连接（即环回连接），并且不能在同一事务中登记。 如果尝试上述操作，连接尝试将被阻止，并且无法将控制权传递回 UDP。 这将导致 UDP 发生超时错误（消息 1206）。  
  
 有关事务和 .NET Framework 的详细信息，请参阅 .NET Framework SDK 中的“执行事务”和“利用事务”。  
  
## <a name="in-this-section"></a>本节内容  
 [事务升级](transaction-promotion.md)  
 介绍提升事务的功能以及如何使用此功能。  
  
 [访问当前事务](accessing-the-current-transaction.md)  
 介绍如何访问当前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上以进程内方式运行的事务。  
  
 [使用 System.Transactions](../native-client-ole-db-transactions/transactions.md)  
 介绍如何在托管应用程序中使用 `System.Transactions` 应用程序编程接口 (API)。  
  
 [事务生存期](transaction-lifetimes.md)  
 介绍分别在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程和 CLR 应用程序中启动的事务生存期的差异。  
  
## <a name="see-also"></a>另请参阅  
 [从 CLR 数据库对象进行数据访问](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
