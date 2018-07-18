---
title: 创建表值参数行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f223bbc3ae87173f98a00dc02f5fc3fcc1d13e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420266"
---
# <a name="table-valued-parameter-rowset-creation"></a>创建表值参数行集
  尽管使用者可以为表值参数提供任意行集对象，但是典型的行集对象要针对后端数据存储来实现，因此提供有限的性能。 有鉴于此，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持使用者在内存中的数据之上创建专用行集对象。 此特殊的内存中的行集对象是新的 COM 对象调用表值参数行集。 它提供与参数集相似的功能。  
  
 表值参数行集对象由使用者通过多个会话级接口为输入参数显式创建。 每个表值参数对应一个表值参数行集对象实例。 使用者可以通过以下两种方法之一创建表值参数行集对象：提供已知的元数据信息（静态方案）；或者通过访问接口发现元数据信息（动态方案）。 以下各节介绍这两种方案。  
  
## <a name="static-scenario"></a>静态方案  
 当已知的类型信息时，使用者使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 来实例化表值参数对应的表值参数行集对象。  
  
 *Guid*字段 (*pTableID*参数) 包含特殊 GUID (CLSID_ROWSET_TVP)。 *PwszName*成员包含使用者要实例化表值参数类型的名称。 *EKind*字段将设置为 DBKIND_GUID_NAME。 此名称在使用特殊 SQL 语句时是必需的，在使用过程调用时是可选的。  
  
 对于聚合，使用者传递*pUnkOuter*参数控制的 IUnknown。  
  
 表值参数行集对象属性只读的因此不应使用者中设置任何属性*rgPropertySets*。  
  
 有关*rgPropertySets*成员的每个 DBCOLUMNDESC 结构，使用者可以指定每个列的其他属性。 这些属性属于 DBPROPSET_SQLSERVERCOLUMN 属性集。 它们支持您为每一列指定计算设置和默认设置。 它们还支持现有列属性，如为空性和标识。  
  
 若要从表值参数行集对象中检索相应的信息，使用者使用 irowsetinfo:: Getproperties。  
  
 若要检索有关 null，唯一的信息计算，并更新每个列的状态，请使用者使用 icolumnsrowset:: Getcolumnsrowset 或 icolumnsinfo:: Getcolumninfo。 以下方法提供有关每个表值参数行集列的详细信息。  
  
 使用者指定表值参数每一列的类型。 这类似于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建表时指定列的方式。 使用者获得从一个表值参数行集对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口通过*ppRowset*输出参数。  
  
## <a name="dynamic-scenario"></a>动态方案  
 如果使用者不具有类型信息，则应使用 iopenrowset:: Openrowset 来实例化表值参数行集对象。 使用者只需向访问接口提供类型名称。  
  
 在此方案中，访问接口代表使用者从服务器获取有关表值参数行集对象的类型信息。  
  
 *PTableID*并*pUnkOuter*应按照静态方案设置参数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口，然后从服务器获取类型信息 （列信息和约束），并返回通过表值参数行集对象*ppRowset*参数。 此操作要求与服务器通信，因此性能不如静态方案。 动态方案仅适用于参数化过程调用。  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [使用表值参数&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
