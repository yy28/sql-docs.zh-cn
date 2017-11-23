---
title: "语句选项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 702aa4a49a3db1c22c90be40486cb212fc1479a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="statement-options"></a>语句选项
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 这些选项允许进行自定义的应用程序中的特定执行语句。  
  
|语句选项|说明|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超过 2,147,483,647 个字节或可用内存。|  
|SQL_CONCURRENCY|允许的值，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|该驱动程序不允许 SQL_CURSOR_DYNAMIC。 请参阅[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)有关详细信息。 允许的值，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|返回一个 32 位整数值，是当前记录号的书签。 仅限; 获取无法设置。|  
|SQL_KEYSET_SIZE|可以设置只为 0。|  
|SQL_MAX_ROWS|要从结果中返回的行最大数目设置。|  
|SQL_ROW_NUMBER|返回一个 32 位整数，指定在结果集中的当前行位置。 仅限; 获取无法设置。|  
|SQL_ROWSET_SIZE|不能超过 4,294,967,296 行;但是，你必须在计算机来处理你的请求中具有足够的虚拟内存。|  
|SQL_USE_BOOKMARKS|支持将 SQL_USE_BOOKMARKS 设置为 SQL_UB_ON，公开固定长度书签。|
