---
title: SQLSetScroll选项（可视化狐狸专业 ODBC 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299417"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持：部分  
  
 ODBC API 符合性：2 级  
  
 设置控制与语句句柄*hstmt*关联的游标行为的选项。  
  
 可视化福克斯Pro ODBC驱动程序仅支持SQL_CONCUR_READ_ONLY;它不支持*fConcurrency*值SQL_CONCUR_ROWVER。 驱动程序将SQL_KEYSET_SIZE、SQL_CURSOR_DYNAMIC和SQL_CURSOR_KEYSET_DRIVEN转换为具有警告ODBC_01S02SQL_SCROLL_STATIC。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetScroll 选项](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。
