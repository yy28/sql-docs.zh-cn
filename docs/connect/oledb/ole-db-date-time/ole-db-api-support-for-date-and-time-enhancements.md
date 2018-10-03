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
manager: craigg
ms.openlocfilehash: 022f7814263067eaa3030ae6c376f99666ad0dd3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695825"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 对日期和时间增强功能的支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|描述|  
|--------------|-----------------|  
|Iaccessor:: Createaccessor|若要启用应用程序区分 DBBINDING 结构中添加了一个标志**datetime**， **datetime2**，并**smalldatetime**值。 有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[大容量复制更改的增强的日期和时间类型&#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|Idbschemarowset:: Getrowset|有关受影响的架构行集的详细信息，请参阅[日期和时间以及架构行集](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|Itabledefinition:: Createtable|有关详细信息，请参阅[OLE DB 日期和时间改进的数据类型支持](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 (OLE DB)](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
