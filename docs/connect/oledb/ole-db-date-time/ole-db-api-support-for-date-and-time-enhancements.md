---
title: 对于日期和时间增强功能的 OLE DB API 支持 |Microsoft 文档
description: 对于日期和时间的增强功能的 OLE DB API 支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b614acdd644369ae3cf04f88edac5a88163e767
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>对于日期和时间增强功能的 OLE DB API 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|使应用程序能够区分 DBBINDING 结构中添加一个标志**datetime**， **datetime2**，和**smalldatetime**值。 有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[增强日期和时间类型的大容量复制更改&#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|受影响的架构行集的详细信息，请参阅[日期和时间以及架构行集](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|ITableDefinition::CreateTable|有关详细信息，请参阅[OLE DB 日期和时间的改进的数据类型支持](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
