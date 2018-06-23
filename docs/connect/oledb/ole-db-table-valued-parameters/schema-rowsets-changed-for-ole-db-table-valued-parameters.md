---
title: 架构行集更改为 OLE DB 表值参数 |Microsoft 文档
description: 更改 OLE DB Table-Valued 参数的架构行集
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
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6eb387969549f0ed72e3635a80fcd6db34852c10
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689830"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>为 OLE DB 表值参数更改的架构行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  以下为已更改或添加以支持表值参数的架构行集。  
  
|架构行集|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|在名为 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMANAME 的行集末尾添加了两个新列。 这些列可供将来的类型重用。 TYPE_NAME 和 LOCAL_TYPE_NAME 列将包含表值参数 TABLE 类型的名称。 DATA_TYPE 列将具有表值参数的值 DBTYPE_TABLE = 143。|  
|DBSCHEMA_TABLE_TYPES|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_TABLES 基本相同，不同的是它仅为表类型而非表、视图或同义词返回元数据。 TABLE_TYPE 列将具有值“TABLE TYPE”。|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_PRIMARY_KEYS 基本相同，不同的是它只为表类型而非表返回主键元数据。|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_COLUMNS 基本相同，不同的是它仅为表类型而非表、视图或同义词返回列元数据。|  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用表值参数&#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
