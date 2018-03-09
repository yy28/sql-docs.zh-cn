---
title: "架构行集更改为 OLE DB 表值参数 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 192a2a0108fa4f54aeaa625f7c812b34edfc75c9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>为 OLE DB 表值参数更改的架构行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  以下为已更改或添加以支持表值参数的架构行集。  
  
|架构行集|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|在名为 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMANAME 的行集末尾添加了两个新列。 这些列可供将来的类型重用。 TYPE_NAME 和 LOCAL_TYPE_NAME 列将包含表值参数 TABLE 类型的名称。 DATA_TYPE 列将具有表值参数的值 DBTYPE_TABLE = 143。|  
|DBSCHEMA_TABLE_TYPES|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_TABLES 基本相同，不同的是它仅为表类型而非表、视图或同义词返回元数据。 TABLE_TYPE 列将具有值“TABLE TYPE”。|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_PRIMARY_KEYS 基本相同，不同的是它只为表类型而非表返回主键元数据。|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_COLUMNS 基本相同，不同的是它仅为表类型而非表、视图或同义词返回列元数据。|  
  
## <a name="see-also"></a>另请参阅  
 [表值参数 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
