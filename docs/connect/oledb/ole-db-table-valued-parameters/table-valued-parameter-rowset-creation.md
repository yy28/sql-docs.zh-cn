---
title: 创建表值参数行集 |Microsoft Docs
description: 创建静态和动态表值参数行集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 2ef87cb742619f163c25bed31b031b85e0e26066
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028186"
---
# <a name="table-valued-parameter-rowset-creation"></a>创建表值参数行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  尽管使用者可以为表值参数提供任意行集对象，但是典型的行集对象要针对后端数据存储来实现，因此提供有限的性能。 因此，适用于 SQL Server 的 OLE DB 驱动程序支持使用者基于内存中的数据创建专用的行集对象。 这种特殊的内存中的行集对象是一种新的 COM 对象，称为表值参数行集。 它提供与参数集相似的功能。  
  
 表值参数行集对象由使用者通过多个会话级接口为输入参数显式创建。 每个表值参数对应一个表值参数行集对象实例。 使用者可以通过以下两种方法之一创建表值参数行集对象：提供已知的元数据信息（静态方案）；或者通过访问接口发现元数据信息（动态方案）。 以下各节介绍这两种方案。  
  
## <a name="static-scenario"></a>静态方案  
 当已知的类型信息时，使用者使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 来实例化表值参数对应的表值参数行集对象。  
  
 *Guid*字段 (*pTableID*参数) 包含特殊 GUID (CLSID_ROWSET_TVP)。 pwszName 成员包含使用者要实例化的表值参数类型的名称。 eKind 字段将设置为 DBKIND_GUID_NAME。 使用特殊 SQL 语句时此名称是必需时，使用过程调用时可选。  
  
 对于聚合，使用者传递*pUnkOuter*参数控制的 IUnknown。  
  
 表值参数行集对象属性只读，因此使用者无需在 rgPropertySets 中设置任何属性。  
  
 对于每个 DBCOLUMNDESC 结构中的 rgPropertySets 成员，使用者可为每列指定附加属性。 这些属性属于 DBPROPSET_SQLSERVERCOLUMN 属性集。 它们支持您为每一列指定计算设置和默认设置。 它们还支持现有列属性，如为空性和标识。  
  
 要从表值参数行集对象中检索相应的信息，使用者应使用 IRowsetInfo::GetProperties。  
  
 若要检索信息为 null，唯一的计算，并更新每个列的状态，使用者可以使用 icolumnsrowset:: Getcolumnsrowset 或 icolumnsinfo:: Getcolumninfo。 以下方法提供有关每个表值参数行集列的详细信息。  
  
 使用者指定表值参数每一列的类型。 这类似于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中创建表时指定列的方式。 使用者为 SQL Server 通过从 OLE DB 驱动程序获取表值参数行集对象*ppRowset*输出参数。  
  
## <a name="dynamic-scenario"></a>动态方案  
 当使用者不具有类型信息时，则应使用 iopenrowset:: Openrowset 来实例化表值参数行集对象。 使用者只需向访问接口提供类型名称。  
  
 在此方案中，访问接口代表使用者从服务器获取有关表值参数行集对象的类型信息。  
  
 *PTableID*并*pUnkOuter*应按照静态方案设置参数。 然后，适用于 SQL Server 的 OLE DB 驱动程序从服务器中获取类型信息（列信息和约束），并通过 ppRowset 参数返回表值参数行集对象。 此操作要求与服务器通信，因此性能不如静态方案。 动态方案仅适用于参数化过程调用。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 (OLE DB)](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 (OLE DB)](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
