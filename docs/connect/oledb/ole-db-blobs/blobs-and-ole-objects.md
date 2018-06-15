---
title: Blob 和 OLE 对象 |Microsoft 文档
description: BLOB 和 OLE 对象
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: cacbe007e9bf0187648ad1fd95c8b6616fb8a300
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666077"
---
# <a name="blobs-and-ole-objects"></a>BLOB 和 OLE 对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驱动程序公开**ISequentialStream**接口以支持对使用者访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**，**文本**，**映像**， **varchar （max)**， **nvarchar (max)**， **varbinary （max)**，和 xml 数据类型作为二进制大型对象 (Blob)。 **读取**方法**ISequentialStream**允许使用者检索的可管理区块中的数据量。  
  
 有关演示此功能的示例，请参阅[设置大型数据&#40;OLE DB&#41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md)。  
  
 SQL Server 的 OLE DB 驱动程序可以使用使用者实现**IStorage**接口时使用者提供在访问器中的接口指针绑定针对数据修改。  
  
 对于大型值数据类型，用于 SQL Server 的 OLE DB 驱动程序检查类型中的大小假设**IRowset**和 DDL 接口。 具有列**varchar**， **nvarchar**，和**varbinary**通过架构行集和将作为 ISLONG 表示数据类型和最大大小设置为无限制返回列数据类型的接口。  
  
 SQL Server 的 OLE DB 驱动程序公开**varchar （max)**， **varbinary （max)** 和**nvarchar (max)** 分别为 DBTYPE_STR、 DBTYPE_BYTES 和 DBTYPE_WSTR 类型。  
  
 若要使用这些类型，应用程序可以使用以下选项：  
  
-   绑定为字节（DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR）。 如果缓冲区不够大，足够截断，将发生完全适用于在以前版本中这些类型 （尽管较大的值现在是可用的）。  
  
-   绑定为字节并指定 DBTYPE_BYREF。  
  
-   绑定为 DBTYPE_IUNKNOWN 并使用流处理。  
  
 如果绑定为 DBTYPE_IUNKNOWN，则使用 ISequentialStream 流功能。 SQL Server 的 OLE DB 驱动程序支持的大型值数据类型为 DBTYPE_IUNKNOWN 绑定输出参数。 这是为了支持存储的过程将这些数据类型作为返回值，将为 DBTYPE_IUNKNOWN 返回到客户端返回其中的方案。  
  
## <a name="storage-object-limitations"></a>存储对象限制  
  
-   SQL Server 的 OLE DB 驱动程序可以支持只有单个打开的存储对象。 尝试打开多个存储对象 (在多个上获取引用**ISequentialStream**接口指针) 返回 DBSTATUS_E_CANTCREATE。  
  
-   OLE DB 驱动程序中的 SQL Server，DBPROP_BLOCKINGSTORAGEOBJECTS 只读属性的默认值是 VARIANT_TRUE。 因此，如果存储对象处于活动状态，某些方法 （而不是存储对象的方法） 将失败并 E_UNEXPECTED。  
  
-   提供由使用者实现的存储对象的数据的长度必须进行已知到 OLE DB 驱动程序的 SQL Server 时创建行访问器引用的存储对象。 使用者必须在用于创建取值函数的 DBBINDING 结构中绑定一个长度指示符。  
  
-   如果某一行包含多个单个大型数据值和 DBPROP_ACCESSORDER 不 DBPROPVAL_AO_RANDOM，使用者必须使用为 SQL Server 支持光标的行集 OLE DB 驱动程序来检索行数据，或者在检索其他之前处理所有的大数据值行值。 如果 DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM，SQL Server 的 OLE DB 驱动程序缓存作为二进制大型对象 (Blob) 的 xml 数据类型，以便可以按任意顺序访问。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [获取大型数据](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [设置大型数据](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 输出参数的流支持](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>请参阅  
 [用于 SQL Server 编程的 OLE DB 驱动程序](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [使用大值类型](../../oledb/features/using-large-value-types.md)  
  
  
