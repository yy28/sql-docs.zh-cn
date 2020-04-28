---
title: SQLSetScrollOptions （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19051fc83466bc40d72c029089cfe6ec45c20a08
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299417"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：部分  
  
 ODBC API 一致性：级别2  
  
 设置控制与语句句柄*hstmt*关联的游标的行为的选项。  
  
 Visual FoxPro ODBC 驱动程序仅支持 SQL_CONCUR_READ_ONLY;它不支持 SQL_CONCUR_ROWVER 的*fConcurrency*值。 驱动程序将 SQL_KEYSET_SIZE、SQL_CURSOR_DYNAMIC 和 SQL_CURSOR_KEYSET_DRIVEN 转换为 SQL_SCROLL_STATIC 并带有警告 ODBC_01S02。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 。
