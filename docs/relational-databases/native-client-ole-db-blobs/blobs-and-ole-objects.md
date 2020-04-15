---
title: BLOB 和 OLE 对象 | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0cb9751940489513f939ab8ee52728c6b75e925
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297621"
---
# <a name="blobs-and-ole-objects"></a>BLOB 和 OLE 对象
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序公开**ISequentialStream**接口，以支持使用者访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext、****文本**、**图像****、varchar（max）、nvarchar（max）、varbinary（max）** 和 xml 数据类型作为二进制大对象 （BLOB）。 **nvarchar(max)** **varbinary(max)** 通过对 ISequentialStream 执行 Read 方法，使用者可以用便于管理的方式成块检索大量数据********。  
  
 有关演示此功能的示例，请参阅[设置大型数据 (OLE DB)](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者在绑定用于数据修改的访问器中提供接口指针时，本机客户端 OLE 数据库提供程序可以使用使用者实现的**IStorage**接口。  
  
 对于较大的值数据类型，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序检查**IRowset**和 DDL 接口中的类型大小假设。 具有**varchar、nvarchar**和**varbinary**数据类型的列，最大大小设置为无限制，将通过返回列数据类型的架构行集和接口表示为 ISLONG。 **nvarchar**  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE DB 提供程序分别将**varchar（最大值**）、varbinary（max） 和**nvarchar（max）** 类型公开为DBTYPE_STR、DBTYPE_BYTES和DBTYPE_WSTR。 **varbinary(max)**  
  
 要使用这些类型的应用程序具有以下选项：  
  
-   绑定为字节（DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR）。 如果缓冲区不够大，将发生截断，这与早期版本中的这些类型完全相同（但是现在可以使用更大的值）。  
  
-   绑定为字节并指定 DBTYPE_BYREF。  
  
-   绑定为 DBTYPE_IUNKNOWN 并使用流处理。  
  
 如果绑定为 DBTYPE_IUNKNOWN，则使用 ISequentialStream 流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序支持绑定输出参数作为大型值数据类型DBTYPE_IUNKNOWN，以方便存储过程将这些数据类型返回为返回值的方案，这些返回值将作为DBTYPE_IUNKNOWN向客户端公开。  
  
## <a name="storage-object-limitations"></a>存储对象限制  
  
-   本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序只能支持单个打开的存储对象。 尝试打开多个存储对象（以获取对多个 ISequentialStream 接口指针的引用）返回 DBSTATUS_E_CANTCREATE****。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序中，DBPROP_BLOCKINGSTORAGEOBJECTS只读属性的默认值VARIANT_TRUE。 这指示如果存储对象处于活动状态，某些方法（存储对象上的方法除外）将失败，并返回 E_UNEXPECTED。  
  
-   创建引用存储对象的行访问器时，必须让[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序知道由使用者实现的存储对象提供的数据长度。 使用者必须在用于创建取值函数的 DBBINDING 结构中绑定一个长度指示符。  
  
-   如果一行包含多个较大的数据值，并且DBPROP_ACCESSORDER未DBPROPVAL_AO_RANDOM，则使用者必须使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序支持游标的行集来检索行数据或在检索其他行值之前处理所有大型数据值。 如果DBPROP_ACCESSORDERDBPROPVAL_AO_RANDOM，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序会将所有 xml 数据类型缓存为二进制大型对象 （BLOB），以便可以按任意顺序访问它。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [获取大型数据](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [设置大型数据](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 输出参数的流支持](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL 服务器本机客户端&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大值类型](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
