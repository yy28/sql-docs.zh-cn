---
title: OLE DB API 对日期和时间增强功能的支持 | Microsoft Docs
description: OLE DB API 对日期和时间增强功能的支持
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c2671b3df6432e63c0e0b36a24bade60286f72a7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015683"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 对日期和时间增强功能的支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|说明|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|DBBINDING 结构中添加了一个标志，可便于应用程序区分 datetime、datetime2 和 smalldatetime 值。 有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[增强型日期和时间类型的大容量复制更改 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|若要详细了解受影响的架构行集，请参阅[日期和时间与架构行集](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|ITableDefinition::CreateTable|有关详细信息，请参阅[针对 OLE DB 日期和时间改进的数据类型支持](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 (OLE DB)](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
