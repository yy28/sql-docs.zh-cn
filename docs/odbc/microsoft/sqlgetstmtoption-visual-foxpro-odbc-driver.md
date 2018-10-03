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
manager: craigg
ms.openlocfilehash: 373f5e13712ef7b0864401ea3d2c204cb03ebb09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646995"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 返回语句选项的当前设置。  
  
|*fOption*|返回|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|为当前记录数的书签的 32 位整数值|  
|SQL_ROW_NUMBER|32 位整数，指定在结果中的当前行的位置设置|  
|SQL_TRANSLATE_DLL|错误:"驱动程序不支持"|  
  
 Visual FoxPro ODBC 驱动程序具有任何转换 Dll。  
  
 有关详细信息，请参阅[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)中*ODBC 程序员参考*。
