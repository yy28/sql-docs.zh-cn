---
title: 适用于 SQL Server 的 OLE DB 驱动程序的稀疏列支持 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序的稀疏列支持
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: f68761672232d2fed88ec3b56d5349d4f925fd43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718305"
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序的稀疏列支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 支持稀疏列。 有关中的稀疏列的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[使用稀疏列](../../../relational-databases/tables/use-sparse-columns.md)并[使用列集](../../../relational-databases/tables/use-column-sets.md)。  
  
 有关 SQL Server 的 OLE DB 驱动程序中的稀疏列支持详细信息[稀疏列支持&#40;OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md)。  
  
 有关演示此功能的示例应用程序的信息，请参阅 [SQL Server 数据编程示例](http://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>稀疏列和适用于 SQL Server 的 OLE DB 驱动程序的用户方案  
 下表总结了常见的用户方案的 OLE DB 驱动程序具有稀疏列的 SQL Server 用户：  
  
|应用场景|行为|  
|--------------|--------------|  
|**选择\*从表**或 iopenrowset:: Openrowset。|返回不是稀疏 column_set 的成员的所有列，以及包含是稀疏 column_set 的成员的所有非空列值的 XML 列。|  
|按名称引用列。|可以不考虑其稀疏列状态或 column_set 成员身份如何而引用列。|  
|通过计算的 XML 列访问 column_set 成员列。|作为稀疏 column_set 的成员的列可以通过按名称选择 column_set 进行访问，并且可通过在 column_set 列中更新 XML 插入和更新值。<br /><br /> 该值必须符合针对 column_set 列的架构。|  
|检索通过 DBSCHEMA_COLUMNS 架构行集表中不含列限制 (OLE DB) 的所有列的元数据。|为不是 column_set 的成员的所有列返回行。 如果该表具有稀疏 column_set，则将为其返回一行。<br /><br /> 请注意，此操作并不返回是 column_set 的成员的列的元数据。|  
|检索所有列的元数据，而不管 column_set 中的稀疏性或成员身份如何。 此操作可能返回大量的行。|为 DBSCHEMA_COLUMNS_EXTENDED 架构行集调用 idbschemarowset:: Getrowset。|  
|只为是 column_set 成员的列检索元数据。 此操作可能返回大量的行。|为 DBSCHEMA_SPARSE_COLUMN_SET 架构行集调用 idbschemarowset:: Getrowset。|  
|确定列是否为稀疏列。|参考 DBSCHEMA_COLUMNS 架构行集 (OLE DB) 的 SS_IS_SPARSE 列。|  
|确定列是否**column_set**。|参考 DBSCHEMA_COLUMNS 架构行集的 SS_IS_COLUMN_SET 列。 或者，参考*dwFlags*由 icolumnsinfo:: Getcolumninfo 或 DBCOLUMNFLAGS 中 icolumnsrowset:: Getcolumnsrowset 返回的行集返回。 对于 column_set 列，将设置 DBCOLUMNFLAGS_SS_ISCOLUMNSET。|  
|为没有 column_set 的表按 BCP 导入和导出稀疏列。|适用于 SQL Server 从早期版本的 OLE DB 驱动程序的行为没有变化。|  
|为有 column_set 的表按 BCP 导入和导出稀疏列。|**Column_set**导入和导出为 XML; 相同的方式，即作为**varbinary （max)** 如果绑定为二进制类型，或与**nvarchar （max)** 如果绑定为**char**或**wchar**类型。<br /><br /> 是稀疏 column_set 的成员的列不导出为非重复列；它们只导出在 column_set 的值中。|  
|**queryout** BCP 的行为。|适用于 SQL Server 的以前版本的 OLE DB 驱动程序从显式命名的列的处理情况没有变化。<br /><br /> 如果应用场景涉及在具有不同架构的表之间进行导入和导出，则可能要求特殊处理。<br /><br /> 有关 BCP 的详细信息，请参阅本章后面的“针对稀疏列的大容量复制 (BCP) 支持”。|  
  
## <a name="down-level-client-behavior"></a>下级客户端行为  
 下级客户端将只为不属于 SQLColumns 和 DBSCHMA_COLUMNS 的稀疏 column_set 的成员的列返回元数据。
  
 下级客户端将按名称访问作为稀疏 column_set 的成员的列，并且 column_set 列将可作为 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 客户端的 XML 列访问。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>针对稀疏列的大容量复制 (BCP) 支持  
 对于稀疏列或 column_set 功能，在 OLE DB 中针对 BCP API 没有任何变化。  
  
 如果某一表具有 column_set，则稀疏列不作为非重复列处理。 值中包含的所有稀疏列的值**column_set**，这导出为 XML 列; 相同的方式，即作为**varbinary （max)** 如果绑定为二进制类型，或与**nvarchar （max)** 如果绑定为**char**或**wchar**类型)。 在导入时， **column_set**值必须符合的架构**column_set**。  
  
 对于 queryout 操作，在处理显式引用的列的方式上没有变化。 column_set 列具有与 XML 列相同的行为，并且稀疏性对于命名稀疏列的处理没有影响。  
  
 但是，如果 queryout 用于导出并且引用的稀疏列属于按名称的稀疏列集的成员，则不能执行向类似结构表的直接导入。 这是因为 BCP 使用与 select 操作一致的元数据进行导入，并且无法将 column_set 成员列与此元数据进行匹配**\***。 若要单独导入 column_set 成员列，必须对引用所需 column_set 列的表定义一个视图，并且必须使用该视图执行导入操作。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/oledb-driver-for-sql-server.md)  
  
  
