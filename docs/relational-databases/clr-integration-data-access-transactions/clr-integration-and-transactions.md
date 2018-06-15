---
title: CLR 集成和事务 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9cab6c061f8baac232563b4afe41952da1b4892e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921552"
---
# <a name="clr-integration-and-transactions"></a>CLR 集成和事务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.Transactions**命名空间提供与 ADO.NET 完全集成的事务框架和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公共语言运行时 (CLR) 集成。 **System.Transactions**和 ADO.NET 共同扩展和简化的本地事务和分布式事务在托管应用程序使用。  
  
> [!NOTE]  
>  CLR 用户定义过程 (UDP) 不能与运行此过程的同一服务器建立连接（即环回连接），并且不能在同一事务中登记。 如果尝试上述操作，连接尝试将被阻止，并且无法将控制权传递回 UDP。 这将导致 UDP 发生超时错误（消息 1206）。  
  
 有关事务和 .NET Framework 的详细信息，请参阅 .NET Framework SDK 中的“执行事务”和“利用事务”。  
  
## <a name="in-this-section"></a>本節內容  
 [事务升级](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 介绍提升事务的功能以及如何使用此功能。  
  
 [访问当前事务](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 介绍如何访问当前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上以进程内方式运行的事务。  
  
 [使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 介绍如何使用**System.Transactions**托管应用程序中的应用程序编程接口 (API)。  
  
 [事务生存期](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 介绍分别在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程和 CLR 应用程序中启动的事务生存期的差异。  
  
## <a name="see-also"></a>另请参阅  
 [从 CLR 数据库对象进行数据访问](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
