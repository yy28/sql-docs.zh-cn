---
title: SQLFreeStmt 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a92af35d8a1b1e98a484c69d7d2e66bf5bef3196
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086082"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 映射
当应用程序*通过 ODBC 1.x*驱动程序调用带有 SQL_DROP*选项*参数的**SQLFreeStmt**时，调用  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 如果将*Handle*参数设置为*hstmt*中的值，则为。
