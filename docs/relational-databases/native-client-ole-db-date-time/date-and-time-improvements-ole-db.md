---
title: 日期和时间改进 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 13409cb079948c4b7956f47dd1b2d9e577ebf6c9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43061417"
---
# <a name="date-and-time-improvements-ole-db"></a>日期和时间改进 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了新的日期和时间数据类型。 本部分介绍如何将这些新类型公开为中的扩展[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端。 概览[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 支持新的日期和时间数据类型，请参阅[日期和时间改进](../../relational-databases/native-client/features/date-and-time-improvements.md)。 有关示例，请参阅[使用增强的日期和时间功能&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)。  
  
 有关日期和时间数据类型的更多常规信息，请参阅[datetime &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [针对 OLE DB 日期和时间改进的数据类型支持](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 提供有关 OLE DB 的信息 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) 类型的支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期和时间数据类型。  
  
 [元数据&#40;OLE DB&#41;](http://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 包含有关 DBBINDING 结构的信息**icommandwithparameters:: Getparameterinfo**， **icommandwithparameters:: Setparameterinfo**， **IColumnsRowset::GetColumnsRowset**，和我**ColumnsInfo::GetColumnInfo**。 还提供了有关 OLE DB 架构行集更新的信息。  
  
 [绑定和转换 (OLE DB)](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 说明在服务器和客户端之间现有和新数据类型的转换规则。  
  
 [增强的日期和时间类型的大容量复制更改&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述支持大容量复制操作的日期/时间增强功能。  
  
 [OLE DB API 对日期和时间增强功能的支持](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 说明支持日期/时间增强功能的 OLE DB API。  
  
 [IRowsetFind 的可比性](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 介绍了日期/时间类型和**IRowsetFind**。  
  
 [新的日期和时间功能与 SQL Server 早期版本&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 说明使用日期和时间增强功能的客户端应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本通信时的预期行为，以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 早期版本编译的客户端向支持日期和时间增强功能的服务器发送命令的预期行为。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
