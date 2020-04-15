---
title: 事务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8779b68d6ab1070514f8ef6685ef378437d09539
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302513"
---
# <a name="transactions"></a>事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序实现本地事务支持。 使用者可借助 Microsoft 分布式事务处理协调器 (MS DTC) 来使用分布式事务或协调事务。 对于需要跨多个会话的事务控制的使用者，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序可以联接 MS DTC 启动和维护的事务。  
  
 默认情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序使用自动提交事务模式，其中使用者会话上的每个离散操作包括针对 实例的完整[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]事务。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序自动提交模式是本地的，并且自动提交事务永远不会超过单个会话。  
  
 本机客户端 OLE 数据库提供程序公开**ITransactionLocal**接口，允许使用者在单个连接上显式和隐式启动到 的实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]事务。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序不支持嵌套本地事务。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [支持本地事务](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [支持分布式事务](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [隔离级别 (OLE DB)](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
