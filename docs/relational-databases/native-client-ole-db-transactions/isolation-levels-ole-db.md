---
title: "隔离级别 (OLE DB) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-transactions
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0e84686dd9c3a8348306d6abbc3969c786002da
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="isolation-levels-ole-db"></a>隔离级别 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端可以控制连接的事务隔离级别。 若要控制事务隔离级别[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序使用者使用：  
  
-   DBPROPSET_SESSION 属性 DBPROP_SESS_AUTOCOMMITISOLEVELS 为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序默认自动提交模式。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]个级别的 Native Client OLE DB 提供程序默认值是 DBPROPVAL_TI_READCOMMITTED。  
  
-   *IsoLevel*参数**ITransactionLocal::StartTransaction**的本地手动提交事务的方法。  
  
-   *IsoLevel*参数**ITransactionDispenser::BeginTransaction**方法为 MS DTC 协调分布式事务。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在脏读隔离级别允许只读访问。 所有其他级别通过将锁应用到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象来限制并发。 当客户端需要更高的并发级别时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会为数据并发访问设置更多限制。 若要维护的并发访问数据，最高级别的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序使用者应智能地控制其请求特定的并发级别。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 引入了快照隔离级别。 有关详细信息，请参阅[使用快照隔离](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [中的](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
