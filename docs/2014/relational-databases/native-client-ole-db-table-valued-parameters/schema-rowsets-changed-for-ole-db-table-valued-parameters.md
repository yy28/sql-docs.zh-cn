---
title: 架构行集更改为 OLE DB 表值参数 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b3769c8279cb439e1fa232b8973e29f117a88e8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026533"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>为 OLE DB 表值参数更改的架构行集
  以下为已更改或添加以支持表值参数的架构行集。  
  
|架构行集|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|在名为 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMANAME 的行集末尾添加了两个新列。 这些列可供将来的类型重用。 TYPE_NAME 和 LOCAL_TYPE_NAME 列将包含表值参数 TABLE 类型的名称。 DATA_TYPE 列将具有表值参数的值 DBTYPE_TABLE = 143。|  
|DBSCHEMA_TABLE_TYPES|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_TABLES 基本相同，不同的是它仅为表类型而非表、视图或同义词返回元数据。 TABLE_TYPE 列将具有值“TABLE TYPE”。|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_PRIMARY_KEYS 基本相同，不同的是它只为表类型而非表返回主键元数据。|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|添加了此行集以支持表值参数。 此行集与 DBSCHEMA_COLUMNS 基本相同，不同的是它仅为表类型而非表、视图或同义词返回列元数据。|  
  
## <a name="see-also"></a>请参阅  
 [表值参数&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [使用表值参数&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  