---
title: OLE DB API 对日期和时间增强功能的支持 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef6334f6fe4671f2563add857f6dd58ce67a2840
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63237849"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 对日期和时间增强功能的支持
  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|说明|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|DBBINDING 结构中添加了一个标志，用于支持应用程序区分 `datetime`、`datetime2` 和 `smalldatetime` 的值。 有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[&#40;OLE DB 和 ODBC&#41;的增强日期和时间类型的大容量复制更改](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|若要详细了解受影响的架构行集，请参阅[日期和时间与架构行集](../native-client-ole-db-rowsets/rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|ITableDefinition::CreateTable|有关详细信息，请参阅[针对 OLE DB 日期和时间改进的数据类型支持](data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 (OLE DB)](date-and-time-improvements-ole-db.md)  
  
  
