---
title: "数据源属性 (OLE DB) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ff8690685f30c0698ba640b599f9f683d4ea854
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="data-source-properties-ole-db"></a>数据源属性 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序实现数据源属性，如下所示。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W：读/写 默认值：无<br /><br /> 描述： DBPROP_CURRENTCATALOG 值报告的当前数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序会话。 设置属性值与当前数据库使用设置的效果相同[!INCLUDE[tsql](../../includes/tsql-md.md)]使用*数据库*语句。<br /><br /> 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，如果你调用[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)和指定的数据库名称在较低的情况下，即使数据库最初创建时混合的案例名，DBPROP_CURRENTCATALOG 将返回名称以小写。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本，DBPROP_CURRENTCATALOG 将返回预期的大小写混合形式。|  
|DBPROP_MULTIPLECONNECTIONS|R/W：读/写 默认值：VARIANT_FALSE<br /><br /> 说明：如果将 DBPROP_MULTIPLECONNECTIONS 设置为 VARIANT_TRUE，当连接运行的命令未生成行集或生成的行集不是服务器游标时，执行其他命令时将新建一个连接，以便执行该命令。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不会创建另一个连接，或如果 DBPROP_MULTIPLECONNECTION 为 VARIANT_FALSE 如果某个事务是活动连接上。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序返回 DB_E_OBJECTOPEN 如果 DBPROP_MULTIPLECONNECTIONS 为 VARIANT_FALSE，并返回 E_FAIL，如果没有活动事务。 事务和锁定是在每个连接的基础上通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来管理的。 如果生成第二个连接，则单独的连接上的命令不共享锁。 若要确保一个命令不会阻塞另一个命令，请对其他命令所请求的行保持锁定。 当创建多个会话时，将同样保持该锁定。<br /><br /> 每个会话都具有一个单独的连接。|  
  
 在提供程序特定属性将设置 DBPROPSET_SQLSERVERDATASOURCE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序定义以下的其他数据源属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W：读/写 默认值：VARIANT_FALSE<br /><br /> 说明：若要从内存启用大容量复制，应将 SSPROP_ENABLEFASTLOAD 属性设置为 VARIANT_TRUE。 通过将数据源上设置此属性，新创建的会话允许使用者访问[IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)接口。<br /><br /> 如果该属性设置为 VARIANT_TRUE， **IRowsetFastLoad**接口是可通过**IOpenRowset::OpenRowset**通过请求**IID_IRowsetFastLoad**接口或通过设置**SSPROP_IRowsetFastLoad**到 VARIANT_TRUE。|  
|SSPROP_ENABLEBULKCOPY|R/W：读/写 默认值：VARIANT_FALSE<br /><br /> 说明：若要从文件启用大容量复制，应将 SSPROP_ENABLEBULKCOPY 属性设置为 VARIANT_TRUE。 对数据源设置该属性之后，使用者可以访问与会话位于同一级别的 IBCPSession 接口。<br /><br /> 此外，还必须将 SSPROP_IRowsetFastLoad 设置为 VARIANT_TRUE。|  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
