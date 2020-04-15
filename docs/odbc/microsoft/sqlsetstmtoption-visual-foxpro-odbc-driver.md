---
title: SQLSetStmtOption（可视化狐狸Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299397"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：1 级  
  
 设置与语句句柄*hstmt*相关的选项。  
  
|*fOption*|允许的值|注释|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|如果尝试设置此*fOption，* 驱动程序将返回错误："驱动程序无法。 Visual FoxPro 不支持异步执行。|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN或 32 位值表示将结果列绑定到的结构或缓冲区实例的长度。||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|驱动程序不允许SQL_CONCUR_ROWVER，因为 Visual FoxPro 没有基于时间戳的行版本控制。|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|驱动程序不允许SQL_CURSOR_KEYSET_DRIVEN或SQL_CURSOR_DYNAMIC;有关详细信息[，请参阅 SQLSetScroll 选项](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md)。|  
|SQL_KEYSET_SIZE|错误："驱动程序无法使用"|Visual FoxPro 不支持键集游标模型。|  
|SQL_MAX_LENGTH|0|如果尝试设置此*fOption*值，驱动程序将返回错误"驱动程序无法。|  
|SQL_MAX_ROWS|0|如果尝试设置此*fOption*值，驱动程序将返回错误"驱动程序无法。|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|如果尝试设置此*fOption*值，驱动程序将返回错误"驱动程序无法。|  
|SQL_RETRIEVE_DATA|SQL_RD_OFFSQL_RD_ON||  
|SQL_ROWSET_SIZE|1 到 4，294，967，296||  
|SQL_SIMULATE_CURSOR|错误："驱动程序无法使用"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetStmtOption。](../../odbc/reference/syntax/sqlsetstmtoption-function.md)
