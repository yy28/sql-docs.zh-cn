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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c2d78e26309d5ea7dc5e6eed5a04e84a1651b33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305739"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：Partial  
  
 ODBC API 一致性：级别 2  
  
 设置用于控制与语句句柄相关联的游标的行为的选项*hstmt*。  
  
 Visual FoxPro ODBC 驱动程序支持仅 SQL_CONCUR_READ_ONLY;它不支持*fConcurrency*值 SQL_CONCUR_ROWVER。 该驱动程序转换为 SQL_KEYSET_SIZE、 SQL_CURSOR_DYNAMIC 和 SQL_CURSOR_KEYSET_DRIVEN SQL_SCROLL_STATIC ODBC_01S02 为警告。  
  
 有关详细信息，请参阅[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)中*ODBC 程序员参考*。
