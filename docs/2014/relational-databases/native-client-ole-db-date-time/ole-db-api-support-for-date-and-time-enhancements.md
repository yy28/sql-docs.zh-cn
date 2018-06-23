---
title: 对于日期和时间增强功能的 OLE DB API 支持 |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2bf7eee4dd2517d4ff9c9f871160ba0515b18ce8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138186"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>对于日期和时间增强功能的 OLE DB API 支持
  以下 OLE DB API 支持日期/时间增强功能。  
  
|函数|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|DBBINDING 结构中添加了一个标志，用于支持应用程序区分 `datetime`、`datetime2` 和 `smalldatetime` 的值。 有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|有关详细信息，请参阅[增强日期和时间类型的大容量复制更改&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|有关详细信息，请参阅[参数和行集元数据](metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|受影响的架构行集的详细信息，请参阅[日期和时间以及架构行集](../native-client-ole-db-rowsets/rowsets.md)。|  
|IRowsetFastLoad|此接口支持新的日期/时间类型，但对其接口没有任何更改。|  
|ITableDefinition::CreateTable|有关详细信息，请参阅[OLE DB 日期和时间的改进的数据类型支持](data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>请参阅  
 [日期和时间改进&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  