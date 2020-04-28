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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299207"
---
# <a name="statement-options"></a>语句选项
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 这些选项允许自定义应用程序中的特定执行语句。  
  
|语句选项|说明|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超过2147483647个字节或可用内存。|  
|SQL_CONCURRENCY|有关允许的值，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|该驱动程序不允许 SQL_CURSOR_DYNAMIC。 有关详细信息，请参阅[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) 。 有关允许的值，请参阅[游标类型和并发组合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|返回一个32位整数值，它是当前记录号的书签。 仅获取;无法设置。|  
|SQL_KEYSET_SIZE|只能设置为0。|  
|SQL_MAX_ROWS|从结果集中返回的最大行数。|  
|SQL_ROW_NUMBER|返回一个32位整数，该整数指定当前行在结果集中的位置。 仅获取;无法设置。|  
|SQL_ROWSET_SIZE|不能超过4294967296行;但是，您的计算机中必须有足够的虚拟内存来处理您的请求。|  
|SQL_USE_BOOKMARKS|支持将 SQL_USE_BOOKMARKS 设置为 SQL_UB_ON 并公开固定长度书签。|
