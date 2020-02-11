---
title: SQLSetStmtOption （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905329"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别1  
  
 设置与语句句柄*hstmt*相关的选项。  
  
|*fOption*|允许的值|注释|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|如果尝试设置此*fOption*，则驱动程序将返回错误： "驱动程序不支持"。 Visual FoxPro 不支持异步执行。|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 或一个32位值，它表示结构的长度或结果列将绑定到的缓冲区的实例。||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|该驱动程序不允许 SQL_CONCUR_ROWVER，因为 Visual FoxPro 没有基于时间戳的行版本控制。|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|该驱动程序不允许 SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC;有关详细信息，请参阅[SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) 。|  
|SQL_KEYSET_SIZE|错误： "驱动程序不能"|Visual FoxPro 不支持键集游标模型。|  
|SQL_MAX_LENGTH|0|如果尝试设置此*fOption*值，驱动程序将返回错误 "驱动程序不支持"。|  
|SQL_MAX_ROWS|0|如果尝试设置此*fOption*值，驱动程序将返回错误 "驱动程序不支持"。|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|如果尝试设置此*fOption*值，驱动程序将返回错误 "驱动程序不支持"。|  
|SQL_RETRIEVE_DATA|SQL_RD_ON，SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1到4294967296||  
|SQL_SIMULATE_CURSOR|错误： "驱动程序不能"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) 。
