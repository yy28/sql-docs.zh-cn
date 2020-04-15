---
title: 语句选项 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299207"
---
# <a name="statement-options"></a>语句选项
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 这些选项允许在应用程序中自定义特定的执行语句。  
  
|语句选项|说明|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超过 2，147，483，647 字节或可用内存。|  
|SQL_CONCURRENCY|有关允许的值，请参阅[光标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|驱动程序不允许SQL_CURSOR_DYNAMIC。 有关详细信息[，请参阅 SQLSetScroll 选项](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)。 有关允许的值，请参阅[光标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|返回作为当前记录编号的书签的 32 位整数值。 只获取;无法设置。|  
|SQL_KEYSET_SIZE|只能设置为 0。|  
|SQL_MAX_ROWS|要从结果集中返回的最大行数。|  
|SQL_ROW_NUMBER|返回一个 32 位整数，指定结果集中当前行的位置。 只获取;无法设置。|  
|SQL_ROWSET_SIZE|不能超过 4，294，967，296 行;但是，您的计算机中必须有足够的虚拟内存来处理您的请求。|  
|SQL_USE_BOOKMARKS|支持将SQL_USE_BOOKMARKS设置为SQL_UB_ON并公开固定长度的书签。|
