---
title: 事务 |Microsoft 文档
description: OLE DB 驱动程序中的 SQL Server 的事务
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd2978ab1778467561c4fab9f246922fb4dfdea2
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="transactions"></a>中的
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序实现的本地事务支持。 使用者可借助 Microsoft 分布式事务处理协调器 (MS DTC) 来使用分布式事务或协调事务。 对于需要跨多个会话的事务控制的用户来说，SQL Server 的 OLE DB 驱动程序可以加入启动和维护的 MS DTC 事务。  
  
 默认情况下，SQL Server 的 OLE DB 驱动程序使用自动提交事务模式，其中每个离散操作的使用者会话上包含实例的完整事务[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 为 SQL Server 自动提交模式 OLE DB 驱动程序是本地计算机，并且自动提交事务永远不会跨越多个单个会话。  
  
 SQL Server 的 OLE DB 驱动程序公开**ITransactionLocal**界面，允许使用显式和隐式在单个连接到的实例上启动事务的使用者[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 SQL Server 的 OLE DB 驱动程序不支持嵌套的本地事务。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [支持本地事务](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [支持分布式事务](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [隔离级别&#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 OLE DB 驱动程序&#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
