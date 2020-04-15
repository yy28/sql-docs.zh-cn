---
title: OLE DB API 对日期和时间增强功能的支持 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1ab4d4956f4a5c54807afd316242cd95ddf6ee7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300981"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 对日期和时间增强功能的支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|说明|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|DBBINDING 结构中添加了一个标志，可便于应用程序区分 datetime****、datetime2**** 和 smalldatetime**** 值。 有关详细信息，请参阅[参数和行集元数据](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[增强日期和时间类型的批量复制更改&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|若要详细了解受影响的架构行集，请参阅[日期和时间与架构行集](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|ITableDefinition::CreateTable|有关详细信息，请参阅[针对 OLE DB 日期和时间改进的数据类型支持](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 (OLE DB)](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
