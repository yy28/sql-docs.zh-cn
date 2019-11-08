---
title: Blob 和 OLE 对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b4e284d2086684af232c17b59675b834b26f497b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790637"
---
# <a name="blobs-and-ole-objects"></a>BLOB 和 OLE 对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**ISequentialStream**接口以支持对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**、 **text**、 **image**、 **varchar （max）** 、 **nvarchar （max）** 、 **varbinary （max）的使用者访问**和 xml 数据类型作为二进制大型对象（blob）。 通过对 ISequentialStream 执行 Read 方法，使用者可以用便于管理的方式成块检索大量数据。  
  
 有关演示此功能的示例，请参阅[Set 大型&#40;Data&#41;OLE DB](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 当使用者在用于数据修改的访问器绑定中提供接口指针时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序可以使用使用者实现的**IStorage**接口。  
  
 对于大值数据类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查**IRowset**和 DDL 接口中的类型大小假设。 使用最大大小设置为 "无限制" 的**varchar**、 **nvarchar**和**varbinary**数据类型的列将通过架构行集和返回列数据类型的接口表示为 ISLONG。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将**varchar （max）** 、 **varbinary （max）** 和**nvarchar （max）** 类型分别公开为 DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR。  
  
 若要使用这些类型，应用程序具有以下选项：  
  
-   绑定为字节（DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR）。 如果缓冲区不够大，将发生截断，这与早期版本中的这些类型完全相同（但是现在可以使用更大的值）。  
  
-   绑定为字节并指定 DBTYPE_BYREF。  
  
-   绑定为 DBTYPE_IUNKNOWN 并使用流处理。  
  
 如果绑定为 DBTYPE_IUNKNOWN，则使用 ISequentialStream 流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持将输出参数绑定为大值数据类型的 DBTYPE_IUNKNOWN，以便于这样的方案：存储过程将这些数据类型作为返回值返回，并将作为 DBTYPE_IUNKNOWN 公开给机.  
  
## <a name="storage-object-limitations"></a>存储对象限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序只能支持一个打开的存储对象。 尝试打开多个存储对象（以获取对多个 ISequentialStream 接口指针的引用）返回 DBSTATUS_E_CANTCREATE。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序中，将 VARIANT_TRUE DBPROP_BLOCKINGSTORAGEOBJECTS 只读属性的默认值。 这指示如果存储对象处于活动状态，某些方法（存储对象上的方法除外）将失败，并返回 E_UNEXPECTED。  
  
-   当创建引用存储对象的行访问器时，必须将由使用者实现的存储对象提供的数据的长度识别为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序。 使用者必须在用于创建取值函数的 DBBINDING 结构中绑定一个长度指示符。  
  
-   如果行包含多个大数据值且未 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER，则使用者必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序游标支持的行集来检索行数据或处理所有大数据值，然后再检索其他行值。 如果 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将所有 xml 数据类型缓存为二进制大型对象（Blob），以便可以按任意顺序访问该数据类型。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [获取大型数据](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [设置大型数据](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 输出参数的流支持](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40;OLE DB&#41; ](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大值类型](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
