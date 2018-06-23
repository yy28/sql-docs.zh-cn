---
title: Blob 和 OLE 对象 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a4c6a32f003206d9d1d92944c3ec8b1a6f48076a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128325"
---
# <a name="blobs-and-ole-objects"></a>BLOB 和 OLE 对象
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**ISequentialStream**接口以支持对使用者访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**，**文本**，**映像**， **varchar （max)**， **nvarchar (max)**， **varbinary （max)**，和 xml 数据类型作为二进制大型对象 (Blob). **读取**方法**ISequentialStream**允许使用者检索的可管理区块中的数据量。  
  
 有关演示此功能的示例，请参阅[设置大型数据&#40;OLE DB&#41;](../native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序可以使用使用者实现**IStorage**接口时使用者提供在访问器中的接口指针绑定针对数据修改。  
  
 对于大型值数据类型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查类型中的大小假设**IRowset**和 DDL 接口。 具有列**varchar**， **nvarchar**，和**varbinary**具有设置为无限制的最大大小的数据类型将通过的架构行集和接口表示为 ISLONG返回列数据类型。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**varchar （max)**， **varbinary （max)** 和**nvarchar (max)** 作为 DBTYPE_STR、 DBTYPE_BYTES 和 DBTYPE_ 类型WSTR 分别。  
  
 可以使用这些类型应用程序，请提供以下选项：  
  
-   绑定为字节（DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR）。 如果缓冲区不够大，将发生截断，这与早期版本中的这些类型完全相同（但是现在可以使用更大的值）。  
  
-   绑定为字节并指定 DBTYPE_BYREF。  
  
-   绑定为 DBTYPE_IUNKNOWN 并使用流处理。  
  
 如果绑定为 DBTYPE_IUNKNOWN，则使用 ISequentialStream 流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持大型值数据类型，以便于其中的存储的过程返回这些数据的方案的 DBTYPE_IUNKNOWN 类型为返回值将公开为 DBTYPE_IUNKNOWN 绑定输出参数向客户端。  
  
## <a name="storage-object-limitations"></a>存储对象限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序可以支持只有单个打开的存储对象。 尝试打开多个存储对象 (在多个上获取引用**ISequentialStream**接口指针) 返回 DBSTATUS_E_CANTCREATE。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序，DBPROP_BLOCKINGSTORAGEOBJECTS 只读属性的默认值是 VARIANT_TRUE。 这指示如果存储对象处于活动状态，某些方法（存储对象上的方法除外）将失败，并返回 E_UNEXPECTED。  
  
-   提供由使用者实现的存储对象的数据的长度必须为公开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序时创建行访问器引用的存储对象。 使用者必须在用于创建取值函数的 DBBINDING 结构中绑定一个长度指示符。  
  
-   如果某一行包含多个单个大型数据值并且 DBPROP_ACCESSORDER 不 DBPROPVAL_AO_RANDOM，使用者必须使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序支持光标的行集检索行数据或处理所有大数据值之前检索其他行值。 如果 DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序作为二进制大型对象 (Blob) 缓存所有 xml 数据类型，以便可以按任意顺序访问。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [获取大型数据](getting-large-data.md)  
  
-   [设置大型数据](setting-large-data.md)  
  
-   [BLOB 输出参数的流支持](streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大值类型](../native-client/features/using-large-value-types.md)  
  
  