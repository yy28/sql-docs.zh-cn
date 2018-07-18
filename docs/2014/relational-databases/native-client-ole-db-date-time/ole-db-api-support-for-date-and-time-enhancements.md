---
title: OLE DB API 对日期和时间增强功能支持 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b94ba91b68daf5415b4c9ae753f4d9e32c6949bc
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408383"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 对日期和时间增强功能的支持
  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|DBBINDING 结构中添加了一个标志，用于支持应用程序区分 `datetime`、`datetime2` 和 `smalldatetime` 的值。 有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[大容量复制更改的增强的日期和时间类型&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|有关受影响的架构行集的详细信息，请参阅[日期和时间以及架构行集](../native-client-ole-db-rowsets/rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|ITableDefinition::CreateTable|有关详细信息，请参阅[OLE DB 日期和时间改进的数据类型支持](data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>请参阅  
 [日期和时间改进&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
