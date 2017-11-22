---
title: "SQLGetStmtOption （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f74b2642ccb5c8b2cae920bcda28561c33e3ff27
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别一个  
  
 返回语句选项的当前设置。  
  
|*FOption*|返回|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|为当前记录号的书签的 32 位整数值|  
|SQL_ROW_NUMBER|指定的结果中的当前行的位置的 32 位整数设置|  
|SQL_TRANSLATE_DLL|错误:"驱动程序不支持"|  
  
 Visual FoxPro ODBC 驱动程序具有不进行转换 Dll。  
  
 有关详细信息，请参阅[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)中*ODBC 程序员参考*。
