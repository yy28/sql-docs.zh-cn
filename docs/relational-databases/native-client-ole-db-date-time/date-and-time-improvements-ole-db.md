---
title: "日期和时间改进 (OLE DB) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9d5e892b42aa8570ceb9fde71e0ed13d351dc53
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="date-and-time-improvements-ole-db"></a>日期和时间改进 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了新的日期和时间数据类型。 本部分介绍如何将这些新类型公开作为中的扩展[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端。 有关概述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端支持新的日期和时间数据类型，请参阅[日期和时间改进](../../relational-databases/native-client/features/date-and-time-improvements.md)。 有关示例，请参阅[使用增强的日期和时间功能 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)。  
  
 有关日期和时间数据类型的更多常规信息，请参阅[datetime &#40;Transact SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>本節內容  
 [针对 OLE DB 日期和时间改进的数据类型支持](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 提供有关 OLE DB 的信息 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端) 类型支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期和时间数据类型。  
  
 [元数据 &#40; OLE DB &#41;](http://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 包含有关 DBBINDING 结构中，信息**ICommandWithParameters::GetParameterInfo**， **ICommandWithParameters::SetParameterInfo**， **IColumnsRowset::GetColumnsRowset**，和我**ColumnsInfo::GetColumnInfo**。 还提供了有关 OLE DB 架构行集更新的信息。  
  
 [绑定和转换 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 说明在服务器和客户端之间现有和新数据类型的转换规则。  
  
 [为增强日期和时间类型 &#40; OLE DB 和 ODBC &#41; 的大容量复制更改](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述支持大容量复制操作的日期/时间增强功能。  
  
 [OLE DB API 对日期和时间增强功能的支持](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 说明支持日期/时间增强功能的 OLE DB API。  
  
 [IRowsetFind 的可比性](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 介绍日期/时间类型和**IRowsetFind**。  
  
 [新的日期和时间功能与以前的 SQL Server 版本 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 说明使用日期和时间增强功能的客户端应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本通信时的预期行为，以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 早期版本编译的客户端向支持日期和时间增强功能的服务器发送命令的预期行为。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
