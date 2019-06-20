---
title: 语句选项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe57ffa0d7628601fcb6dd19218715b32a57322b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270015"
---
# <a name="statement-options"></a>语句选项
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 这些选项允许自定义应用程序中的特定执行语句。  
  
|语句选项|说明|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超过 2,147,483,647 个字节或可用内存。|  
|SQL_CONCURRENCY|允许的值，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|该驱动程序不允许 SQL_CURSOR_DYNAMIC。 请参阅[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)有关详细信息。 允许的值，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|返回是当前的记录号的书签将变为一个 32 位整数值。 仅限; 获取不能设置。|  
|SQL_KEYSET_SIZE|可以设置只为 0。|  
|SQL_MAX_ROWS|设置要从结果中返回的行的最大数。|  
|SQL_ROW_NUMBER|返回指定结果集内的当前行的位置的 32 位整数。 仅限; 获取不能设置。|  
|SQL_ROWSET_SIZE|不能超过 4,294,967,296 行;但是，您必须具有足够的虚拟内存来处理你的请求在计算机中。|  
|SQL_USE_BOOKMARKS|支持将 SQL_USE_BOOKMARKS 设置为 SQL_UB_ON 并公开固定长度的书签。|
