---
title: "datetime 数据类型转换 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 065c030e38e588dbc1068ead291f0ac4f5a6a179
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="datetime-data-type-conversions-odbc"></a>datetime 数据类型转换 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  以下转换或者已由 ODBC 定义，或者是 ODBC 的一致扩展。 每个访问接口提供的转换由该访问接口所服务的社区决定，因此，各个访问接口之间通常不一致。 方括号中的值是可选的。  
  
-   日期时间字符串的格式为 'yyyy-mm-dd[ hh:mm:ss[.9999999][ 加/减 hh:mm]]'  
  
-   时间字符串的格式为 'hh:mm:ss[.9999999]'  
  
-   日期字符串的格式为 'yyyy-mm-dd'  
  
 从字符串转换允许更灵活处理空格和字段宽度。 有关详细信息，请参阅的"数据格式:: 字符串和文本"部分[ODBC 日期和时间的改进的数据类型支持](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)。  
  
 下面是一般的转换规则：  
  
-   如果未提供时间但接收方可存储时间，则将时间设置为零。  
  
-   如果不存在日期但接收方可以存储日期，则使用当前日期。  
  
-   如果客户端正在使用的数据类型中不存在时区，但服务器可以存储时区，则在客户端时区中存储日期。 请注意，此行为与服务器行为不同。  
  
-   如果服务器类型中不存在时区，但客户端类型具有时区，则先将时间转换为 UTC，再将其存储到服务器。  
  
-   如果存在时间但接收方无法存储时间，则忽略时间部分。  
  
-   如果存在日期但接收方无法存储日期，则忽略日期部分。  
  
-   如果在从 C 转换到 SQL 时截断了秒或秒的小数部分，则生成带有 SQLSTATE 22008 的诊断记录和消息“日期时间字段溢出”。  
  
-   如果在从 SQL 转换到 C 时截断了秒或秒的小数部分，则生成带有 SQLSTATE 01S07 的诊断记录和消息“截断小数部分”。  
  
## <a name="in-this-section"></a>本节内容  
 [从 C 到 SQL 转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)  
 列出了在从 C 类型转换到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/时间类型时要考虑的问题。  
  
 [从 SQL 转换到 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)  
 列出了在从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/时间类型转换到 C 类型时要考虑的问题。  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
