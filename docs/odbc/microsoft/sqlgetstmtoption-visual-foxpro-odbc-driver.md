---
title: SQLGetStmtOption （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898787"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：一级  
  
 返回语句选项的当前设置。  
  
|*FOption*|返回|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|32位整数值，它是当前记录号的书签|  
|SQL_ROW_NUMBER|32位整数，用于指定结果集中当前行的位置|  
|SQL_TRANSLATE_DLL|错误： "驱动程序不能"|  
  
 Visual FoxPro ODBC 驱动程序没有转换 Dll。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 。
