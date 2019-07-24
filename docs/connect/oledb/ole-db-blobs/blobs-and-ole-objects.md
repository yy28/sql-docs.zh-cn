---
title: Blob 和 OLE 对象 |Microsoft Docs
description: BLOB 和 OLE 对象
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 70d3ffccfc9613434b09335944e445a2705b95c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988668"
---
# <a name="blobs-and-ole-objects"></a>BLOB 和 OLE 对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序公开 ISequentialStream 接口，以便支持使用者访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ntext、text、image、varchar(max)、nvarchar(max)、varbinary(max) 和作为二进制大型对象 (BLOB) 的 xml 数据类型        。 通过对 ISequentialStream 执行 Read 方法，使用者可以用便于管理的方式成块检索大量数据   。  
  
 有关演示此功能的示例, 请参阅[Set 大型&#40;Data&#41;OLE DB](../../oledb/ole-db-how-to/set-large-data-ole-db.md)。  
  
 当使用者在数据修改绑定的取值函数中提供接口指针时，适用于 SQL Server 的 OLE DB 驱动程序可以使用由使用者实现的 IStorage 接口  。  
  
 对于大值数据类型，适用于 SQL Server 的 OLE DB 驱动程序检查 IRowset 和 DDL 接口中的类型大小假设  。 具有 varchar、nvarchar 和 varbinary 数据类型且最大大小设置为无限制的列将通过架构行集和返回列数据类型的接口表示为 ISLONG    。  
  
 适用于 SQL Server 的 OLE DB 驱动程序将 varchar(max)、varbinary(max) 和 nvarchar(max) 类型分别公开为 DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR    。  
  
 若要使用这些类型，应用程序可以使用以下选项：  
  
-   绑定为字节（DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR）。 如果缓冲区不够大，将发生截断，这与早期版本中的这些类型完全相同（但是现在可以使用更大的值）。  
  
-   绑定为字节并指定 DBTYPE_BYREF。  
  
-   绑定为 DBTYPE_IUNKNOWN 并使用流处理。  
  
 如果绑定为 DBTYPE_IUNKNOWN，则使用 ISequentialStream 流功能。 SQL Server 的 OLE DB 驱动程序支持将输出参数绑定为大值数据类型的 DBTYPE_IUNKNOWN。 这是为了支持存储过程以返回值的形式返回这些数据类型的情况, 返回值将以 DBTYPE_IUNKNOWN 的形式返回到客户端。  
  
## <a name="storage-object-limitations"></a>存储对象限制  
  
-   SQL Server 的 OLE DB 驱动程序只能支持一个打开的存储对象。 尝试打开多个存储对象（以获取对多个 ISequentialStream 接口指针的引用）返回 DBSTATUS_E_CANTCREATE  。  
  
-   在适用于 SQL Server 的 OLE DB 驱动程序中，DBPROP_BLOCKINGSTORAGEOBJECTS 只读属性的默认值为 VARIANT_TRUE。 因此，如果存储对象处于活动状态，某些方法（存储对象上的方法除外）将失败，并返回 E_UNEXPECTED。  
  
-   当创建引用由使用者实现的存储对象的行取值函数时，适用于 SQL Server 的 OLE DB 驱动程序必须了解该存储对象提供的数据长度。 使用者必须在用于创建取值函数的 DBBINDING 结构中绑定一个长度指示符。  
  
-   如果行包含多个大型数据值，且 DBPROP_ACCESSORDER 不为 DBPROPVAL_AO_RANDOM，使用者必须使用支持适用于 SQL Server 的 OLE DB 驱动程序游标的行集来检索行数据，或在检索其他行值之前处理所有大型数据值。 如果 DBPROP_ACCESSORDER 为 DBPROPVAL_AO_RANDOM，适用于 SQL Server 的 OLE DB 驱动程序将所有 xml 数据类型缓存为二进制大型对象 (BLOB)，以便以任意顺序进行访问。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [获取大型数据](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [设置大型数据](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 输出参数的流支持](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [使用大值类型](../../oledb/features/using-large-value-types.md)  
  
  
