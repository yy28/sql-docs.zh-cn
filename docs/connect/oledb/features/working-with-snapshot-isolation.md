---
title: 使用快照隔离 |Microsoft 文档
description: 使用 OLE DB 驱动程序中的 SQL Server 的快照隔离
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], snapshot isolation
- MSOLEDBSQL, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, snapshot isolation
- SQLGetInfo function
- concurrency [OLE DB Driver for SQL Server]
- SQLSetConnectAttr function
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 5f48c0faf0f5eeb8777151c6c3642cedcacb09b9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-snapshot-isolation"></a>使用快照隔离
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了旨在增强联机事务处理 (OLTP) 应用程序的并发处理能力的新“快照”隔离级别。 在早期版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，并发仅基于锁定，对于某些应用程序，这可能导致阻塞和死锁问题。 快照隔离依赖于行版本控制的增强功能，旨在通过避免读取器-编写器阻塞情况来提高性能。  
  
 在快照隔离下启动的事务读取该事务启动时的数据库快照。 键集，动态和静态服务器游标，在快照事务上下文中打开的行为类似于非常类似于静态游标可序列化事务中打开。 但是，当在打开游标时不会采取的快照隔离级别的锁。 这一事实可以减少服务器上的阻碍。  
  
## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序  
 SQL Server 的 OLE DB 驱动程序已利用的快照隔离中引入的增强功能[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 这些增强功能包括对 DBPROPSET_DATASOURCEINFO 和 DBPROPSET_SESSION 属性集的更改。  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 已更改 DBPROPSET_DATASOURCEINFO 属性集，以便指示通过添加在 DBPROP_SUPPORTEDTXNISOLEVELS 中使用的 DBPROPVAL_TI_SNAPSHOT 值来支持快照隔离级别。 此新值指示支持快照隔离级别，而不管是否对数据库启用了版本控制。 下表列出 DBPROP_SUPPORTEDTXNISOLEVELS 值：  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|类型：VT_I4<br /><br /> R/W：只读<br /><br /> 说明：指定支持的事务隔离级别的位掩码。 零个或多个下列各项的组合：<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 已更改 DBPROPSET_SESSION 属性集，以便指示通过添加在 DBPROP_SESS_AUTOCOMMITISOLEVELS 中使用的 DBPROPVAL_TI_SNAPSHOT 值来支持快照隔离级别。 此新值指示支持快照隔离级别，而不管是否对数据库启用了版本控制。 下表列出 DBPROP_SESS_AUTOCOMMITISOLEVELS 值：
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|类型：VT_I4<br /><br /> R/W：只读<br /><br /> 说明：指定指示在自动提交模式下的事务隔离级别的位掩码。 可以设置此位掩码中的值是可以为 DBPROP_SUPPORTEDTXNISOLEVELS 设置的值相同。|  
  
> [!NOTE]  
>  如果在使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本时设置 DBPROPVAL_TI_SNAPSHOT，将发生 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED 错误。  
  
 有关如何在事务中支持快照隔离的信息，请参阅[支持本地事务](../../oledb/ole-db-transactions/supporting-local-transactions.md)。  

  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [行集属性和行为](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
