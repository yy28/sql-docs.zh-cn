---
title: SQLSetCursorName （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab3e9a0ee13cca4950ec7797b2cebed3a0437f55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905468"
---
# <a name="sqlsetcursorname-visual-foxpro-odbc-driver"></a>SQLSetCursorName（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 将游标名称与活动语句句柄*hstmt*关联。 **SQLSetCursorName**包含在 VISUAL FoxPro Odbc 驱动程序 API 中，因为它是核心级 odbc API 功能的一部分;它无法与其他 API 函数一起使用，因为该驱动程序不支持定位更新。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLSetCursorName](../../odbc/reference/syntax/sqlsetcursorname-function.md) 。
