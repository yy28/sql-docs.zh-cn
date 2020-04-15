---
title: SQLSetCursor 名称（可视化狐狸 Pro ODBC 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 2ac5a8b5-f084-405b-b0d7-546284dfa111
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89bc77d12a4966762fa3aa2cf8b702ca6b47ac6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306122"
---
# <a name="sqlsetcursorname-visual-foxpro-odbc-driver"></a>SQLSetCursorName（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 将游标名称与活动语句句柄*hstmt*关联。 **SQLSetCursorName**包含在 Visual FoxPro ODBC 驱动程序 API 中，因为它是核心级 ODBC API 功能的一部分;它不能与其他 API 函数一起使用，因为驱动程序不支持定位更新。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetCursorName。](../../odbc/reference/syntax/sqlsetcursorname-function.md)
