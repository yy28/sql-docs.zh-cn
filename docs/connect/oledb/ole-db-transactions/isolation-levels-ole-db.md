---
title: 隔离级别 (OLE DB) |Microsoft 文档
description: 隔离级别 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.workload: Inactive
ms.openlocfilehash: 03612c759cd25eb280573fa172ef86691f58dc19
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="isolation-levels-ole-db"></a>隔离级别 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端可以控制连接的事务隔离级别。 若要控制事务隔离级别，OLE DB 驱动程序的 SQL Server 使用者使用：  
  
-   DBPROPSET_SESSION 属性 DBPROP_SESS_AUTOCOMMITISOLEVELS OLE DB 驱动程序为 SQL Server 默认自动提交模式。  
  
     SQL Server 级别的默认值为 OLE DB 驱动程序是 DBPROPVAL_TI_READCOMMITTED。  
  
-   *IsoLevel*参数**ITransactionLocal::StartTransaction**的本地手动提交事务的方法。  
  
-   *IsoLevel*参数**ITransactionDispenser::BeginTransaction**方法为 MS DTC 协调分布式事务。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在脏读隔离级别允许只读访问。 所有其他级别通过将锁应用到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象来限制并发。 当客户端需要更高的并发级别时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 会为数据并发访问设置更多限制。 若要维护最高级别的数据的并发访问权限，OLE DB 驱动程序的 SQL Server 使用者应智能地控制其请求特定的并发级别。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了快照隔离级别。 有关详细信息，请参阅[使用快照隔离](../../oledb/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [事务](../../oledb/ole-db-transactions/transactions.md)  
  
  
