---
title: 表值参数行集创建 |Microsoft 文档
description: 静态和动态表值参数行集创建
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e15a1a49bad22ca909b6e05a6d635a15dac93dd
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="table-valued-parameter-rowset-creation"></a>创建表值参数行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  尽管使用者可以为表值参数提供任意行集对象，但是典型的行集对象要针对后端数据存储来实现，因此提供有限的性能。 因此，SQL Server 的 OLE DB 驱动程序允许使用者创建基于内存中数据的专用化的行集对象。 这种特殊的内存中的行集对象是一种新的 COM 对象，称为表值参数行集。 它提供与参数集相似的功能。  
  
 表值参数行集对象由使用者通过多个会话级接口为输入参数显式创建。 没有每个表值参数的表值参数行集对象的一个实例。 使用者可以通过以下两种方法之一创建表值参数行集对象：提供已知的元数据信息（静态方案）；或者通过访问接口发现元数据信息（动态方案）。 以下各节介绍这两种方案。  
  
## <a name="static-scenario"></a>静态方案  
 当已知的类型信息时，使用者将使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 来实例化都对应于表值参数的表值参数行集对象。  
  
 *Guid*字段 (*pTableID*参数) 包含特殊的 GUID (CLSID_ROWSET_TVP)。 *PwszName*成员包含使用者要实例化表值参数类型的名称。 *EKind*字段将设置为 DBKIND_GUID_NAME。 此名称是必需的该语句时临时 SQL;名称是可选的如果它是一个过程调用的。  
  
 对于聚合，使用者将传递*pUnkOuter*控制 IUnknown 参数。  
  
 表值参数行集对象属性只读字段，以便使用者不需要在中设置任何属性*rgPropertySets*。  
  
 有关*rgPropertySets*的每个 DBCOLUMNDESC 结构，使用者的成员可以指定每个列的其他属性。 这些属性属于 DBPROPSET_SQLSERVERCOLUMN 属性集。 它们支持您为每一列指定计算设置和默认设置。 它们还支持现有列属性，如为空性和标识。  
  
 若要从表值参数行集对象中检索相应的信息，使用者，请使用 IRowsetInfo::GetProperties。  
  
 若要检索有关 null，唯一的信息计算，并更新每个列的状态，请使用者可以使用 IColumnsRowset::GetColumnsRowset 或 IColumnsInfo::GetColumnInfo。 以下方法提供有关每个表值参数行集列的详细信息。  
  
 使用者指定表值参数每一列的类型。 它是类似于列中创建表时的指定方式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 使用者将表值参数行集对象从 OLE DB 驱动程序获取适用于 SQL Server 通过*ppRowset*输出参数。  
  
## <a name="dynamic-scenario"></a>动态方案  
 当使用者没有类型信息时，它应使用 IOpenRowset::OpenRowset 来实例化表值参数行集对象。 使用者只需向访问接口提供类型名称。  
  
 在此方案中，访问接口代表使用者从服务器获取有关表值参数行集对象的类型信息。  
  
 *PTableID*和*pUnkOuter*参数应设置如下所示的静态方案。 SQL Server 的 OLE DB 驱动程序，然后在服务器上，获取类型信息 （列信息和约束），并返回表值参数行集对象，通过*ppRowset*参数。 此操作需要与服务器通信，并因此不会执行以及静态的方案。 动态方案仅适用于参数化过程调用。  
  
## <a name="see-also"></a>另请参阅  
 [表值参数&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 &#40; OLE DB &#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
