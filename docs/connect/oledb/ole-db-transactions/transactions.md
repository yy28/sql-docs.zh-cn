---
title: 事务 | Microsoft Docs
description: OLE DB Driver for SQL Server 中的事务
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 64a05f57c40027a4db448a987d32f77d62f0a837
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011229"
---
# <a name="transactions"></a>事务
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 实现本地事务支持。 使用者可借助 Microsoft 分布式事务处理协调器 (MS DTC) 来使用分布式事务或协调事务。 对于需要跨多个会话的事务控制权的使用者，适用于 SQL Server 的 OLE DB 驱动程序可以加入由 MS DTC 启动和维护的事务。  
  
 默认情况下，适用于 SQL Server 的 OLE DB 驱动程序使用自动提交事务模式，其中对使用者会话执行的每次离散操作均包含一个针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的完整事务。 适用于 SQL Server 的 OLE DB 驱动程序的自动提交模式是本地的，并且自动提交事务从不会跨多个会话。  
  
 适用于 SQL Server 的 OLE DB 驱动程序公开 ITransactionLocal 接口，并允许使用者在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的单个连接上使用显式和隐式启动事务。 OLE DB Driver for SQL Server 不支持嵌套的本地事务。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [支持本地事务](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [支持分布式事务](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [隔离级别 (OLE DB)](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
