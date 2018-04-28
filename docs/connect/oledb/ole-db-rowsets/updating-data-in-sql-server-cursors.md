---
title: 更新 SQL Server 游标中的数据 |Microsoft 文档
description: 更新 SQL Server 游标中的数据
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97c03835408ef89cb3940f951f117640e5b432fe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updating-data-in-sql-server-cursors"></a>更新 SQL Server 游标中的数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  当提取和更新数据通过[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]游标，用于使用者应用程序受相同的注意事项和约束应用于任何其他客户端应用程序的 SQL Server 的 OLE DB 驱动程序。  
  
 只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标中的行才参与并发数据访问控制。 当使用者请求可修改的行集时，并发控制是通过 DBPROP_LOCKMODE 控制的。 若要修改并发访问控制的级别，使用者应在打开该行集之前设置 DBPROP_LOCKMODE 属性。  
  
 如果客户端应用程序设计使事务长时间保持打开状态，事务隔离级别在定位行时可能造成严重滞后。 默认情况下，SQL Server 的 OLE DB 驱动程序使用 DBPROPVAL_TI_READCOMMITTED 由指定的已提交读隔离级别。 SQL Server 的 OLE DB 驱动程序支持脏读的隔离时的行集并发是只读的。 因此，使用者可以在可修改行集中请求更高级别的隔离，但是不能成功请求任何更低级别。  
  
## <a name="immediate-and-delayed-update-modes"></a>立即更新模式和延迟更新模式  
 在立即更新模式下，每个调用到**IRowsetChange::SetData**导致到往返行程[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如果使用者发出到单个行的多个更改，它会将与单个的所有更改都提交更加高效**SetData**调用。  
  
 在延迟的更新模式下，进行一次往返[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中指明了每个行*cRows*和*rghRows*参数**IRowsetUpdate::Update**。  
  
 无论哪种模式，往返表示当未针对行集打开事务对象时的不同事务。  
  
 如果要使用**IRowsetUpdate::Update**，SQL Server 的 OLE DB 驱动程序尝试处理每个指定的行。 由于任何行的无效数据、 长度或状态的值发生错误不会停止 SQL Server 处理 OLE DB 驱动程序。 可能修改参与更新的所有其他行，也可能不修改这些行。 使用者必须检查返回*prgRowStatus*数组以 SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 时确定的任何特定行失败。  
  
 使用者不应假定行以任意特定顺序处理。 如果使用者要求按顺序处理基于多个行的数据修改，使用者应在应用程序逻辑中建立该顺序，并打开一个事务以包含该过程。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集合中的数据](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
