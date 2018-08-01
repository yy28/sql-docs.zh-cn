---
title: 隔离级别 (OLE DB) |Microsoft Docs
description: 隔离级别 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: bc4b60a56b5c12ac040c1b1481660175154c880f
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109669"
---
# <a name="isolation-levels-ole-db"></a>隔离级别 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端可以控制连接的事务隔离级别。 若要控制事务隔离级别，为 SQL Server 使用者，OLE DB 驱动程序使用：  
  
-   将 DBPROPSET_SESSION 属性 DBPROP_SESS_AUTOCOMMITISOLEVELS 用于适用于 SQL Server 的 OLE DB 驱动程序默认自动提交模式。  
  
     OLE DB 驱动程序的 SQL Server 默认级别是 DBPROPVAL_TI_READCOMMITTED。  
  
-   将 ITransactionLocal::StartTransaction 方法的 isoLevel 参数用于本地手动提交事务。  
  
-   将 ITransactionDispenser::BeginTransaction 方法的 isoLevel 参数用于 MS DTC 协调的分布式事务。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在脏读隔离级别允许只读访问。 所有其他级别通过将锁应用到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象来限制并发。 当客户端需要更高的并发级别时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 会为数据并发访问设置更多限制。 若要维护最高级别的数据并发访问，适用于 SQL Server 的 OLE DB 驱动程序使用者应对特定并发级别请求进行智能控制。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了快照隔离级别。 有关详细信息，请参阅[使用快照隔离](../../oledb/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [中的](../../oledb/ole-db-transactions/transactions.md)  
  
  
