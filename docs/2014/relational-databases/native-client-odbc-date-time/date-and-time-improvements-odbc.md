---
title: 日期和时间改进 (ODBC) |Microsoft 文档
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
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 19c4e63fc9e101379af2ac7b6bc859daa783ae6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137961"
---
# <a name="date-and-time-improvements-odbc"></a>日期和时间改进 (ODBC)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了新的日期和时间数据类型。 本部分介绍如何将这些新类型公开作为中的扩展[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端。 有关概述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端支持新的日期和时间数据类型，请参阅[日期和时间改进](../native-client/features/date-and-time-improvements.md)。 有关示例，演示 ODBC 日期/时间支持，请参阅[使用日期和时间类型](../native-client-odbc-how-to/use-date-and-time-types.md)。  
  
 有关日期和时间数据类型的更多常规信息，请参阅[datetime &#40;TRANSACT-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)。  
  
## <a name="in-this-section"></a>本节内容  
 [针对 ODBC 日期/时间改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 提供有关支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和时间数据类型的 ODBC 类型的信息。  
  
 [元数据&#40;ODBC&#41;](../../database-engine/dev-guide/metadata-odbc.md)  
 描述在实现参数描述符 (IPD) 和实现行描述符 (IRD) 字段中返回的信息，以及由 `SQLColumns` 和 `SQLProcedureColumns` 返回的列元数据。 还描述了由 `SQLGetTypeInfo` 返回的数据类型元数据。  
  
 [datetime 数据类型转换&#40;ODBC&#41;](datetime-data-type-conversions-odbc.md)  
 描述如何在 datetime 值和 datetimeoffset 值之间进行转换。  
  
 [sql_variant 对日期和时间类型的支持](sql-variant-support-for-date-and-time-types.md)  
 描述用于获得增强的日期和时间功能的 SQL_VARIANT 函数支持。  
  
 [增强的日期和时间类型进行大容量复制更改&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述支持大容量复制操作的日期/时间增强功能。  
  
 [增强的日期和时间类型与以前的 SQL Server 版本的行为&#40;ODBC&#41;](enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 描述使用日期和时间增强功能的客户端应用程序与早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通信时的预期行为，以及使用早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 编译的客户端向支持日期和时间增强功能的服务器发送命令时的预期行为。  
  
 [ODBC API 对日期和时间增强功能的支持](odbc-api-support-for-enhanced-date-and-time-features.md)  
 列出了支持日期和时间增强功能的 ODBC 函数。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
