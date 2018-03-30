---
title: 数据源属性 (OLE DB) |Microsoft 文档
description: 数据源属性 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c66917b1b62ef19ea4a36bed1644ee90eefa954
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="data-source-properties-ole-db"></a>数据源属性 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序，如下所示实现数据源属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W：读/写 默认值：无<br /><br /> 描述： DBPROP_CURRENTCATALOG 的值将报告当前数据库 OLE DB 驱动程序的 SQL Server 会话。 设置属性值与当前数据库使用设置的效果相同[!INCLUDE[tsql](../../../includes/tsql-md.md)]使用*数据库*语句。<br /><br /> 开头[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，如果你调用[sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)和指定的数据库名称在较低的情况下，即使数据库最初创建时混合的案例名，DBPROP_CURRENTCATALOG 将返回名称以小写。 对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的早期版本，DBPROP_CURRENTCATALOG 将返回预期的大小写混合形式。|  
|DBPROP_MULTIPLECONNECTIONS|R/W：读/写 默认值：VARIANT_FALSE<br /><br /> 说明：如果将 DBPROP_MULTIPLECONNECTIONS 设置为 VARIANT_TRUE，当连接运行的命令未生成行集或生成的行集不是服务器游标时，执行其他命令时将新建一个连接，以便执行该命令。<br /><br /> SQL Server 的 OLE DB 驱动程序不会创建另一个连接，或如果 DBPROP_MULTIPLECONNECTION 为 VARIANT_FALSE 如果某个事务是活动连接上。 SQL Server 的 OLE DB 驱动程序返回 DB_E_OBJECTOPEN 如果 DBPROP_MULTIPLECONNECTIONS 为 VARIANT_FALSE，并返回 E_FAIL，如果没有活动事务。 事务和锁定是在每个连接的基础上通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 来管理的。 如果生成第二个连接，则单独的连接上的命令不共享锁。 若要确保一个命令不会阻塞另一个命令，请对其他命令所请求的行保持锁定。 当创建多个会话时，将同样保持该锁定。<br /><br /> 每个会话都具有一个单独的连接。|  
  
 在提供程序特定属性集 DBPROPSET_SQLSERVERDATASOURCE 中，SQL Server 的 OLE DB 驱动程序定义的以下的其他数据源属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W：读/写 默认值：VARIANT_FALSE<br /><br /> 说明：若要从内存启用大容量复制，应将 SSPROP_ENABLEFASTLOAD 属性设置为 VARIANT_TRUE。 通过将数据源上设置此属性，新创建的会话允许使用者访问[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)接口。<br /><br /> 如果该属性设置为 VARIANT_TRUE， **IRowsetFastLoad**接口是可通过**IOpenRowset::OpenRowset**通过请求**IID_IRowsetFastLoad**接口或通过设置**SSPROP_IRowsetFastLoad**到 VARIANT_TRUE。|  
|SSPROP_ENABLEBULKCOPY|R/W：读/写 默认值：VARIANT_FALSE<br /><br /> 说明：若要从文件启用大容量复制，应将 SSPROP_ENABLEBULKCOPY 属性设置为 VARIANT_TRUE。 对数据源设置该属性之后，使用者可以访问与会话位于同一级别的 IBCPSession 接口。<br /><br /> 此外，还必须将 SSPROP_IRowsetFastLoad 设置为 VARIANT_TRUE。|  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象 &#40; OLE DB &#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
