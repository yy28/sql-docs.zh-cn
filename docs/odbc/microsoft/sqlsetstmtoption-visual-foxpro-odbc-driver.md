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
manager: craigg
ms.openlocfilehash: 9d7bcecfbd880f53d1067fd68202b62c34fce398
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305823"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：级别 1  
  
 设置与语句句柄，相关的选项*hstmt*。  
  
|*fOption*|允许的值|注释|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|如果你尝试将此项设置*fOption*，驱动程序将返回错误："驱动程序不支持"。 Visual FoxPro 不支持异步执行。|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN 或表示的结构或列将绑定到的结果的缓冲区的实例的长度为 32 位值。||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|该驱动程序不允许 SQL_CONCUR_ROWVER，因为 Visual FoxPro 不具有基于时间戳的行版本控制。|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|该驱动程序不允许 SQL_CURSOR_KEYSET_DRIVEN 或 SQL_CURSOR_DYNAMIC;请参阅[SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md)有关详细信息。|  
|SQL_KEYSET_SIZE|错误："驱动程序不支持"|Visual FoxPro 不支持由键集游标模型。|  
|SQL_MAX_LENGTH|0|如果你尝试将此项设置*fOption*值，该驱动程序返回错误"驱动程序不支持"。|  
|SQL_MAX_ROWS|0|如果你尝试将此项设置*fOption*值，该驱动程序返回错误"驱动程序不支持"。|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|如果你尝试将此项设置*fOption*值，该驱动程序返回错误"驱动程序不支持"。|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 到 4294967296||  
|SQL_SIMULATE_CURSOR|错误："驱动程序不支持"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 有关详细信息，请参阅[SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)中*ODBC 程序员参考*。
