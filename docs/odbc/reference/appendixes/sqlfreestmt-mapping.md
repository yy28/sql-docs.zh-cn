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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086082"
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 映射
当应用程序调用**SQLFreeStmt**与*选项*参数通过 ODBC SQL_DROP *3.x*驱动程序，将会调用  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 与*处理*参数设置为中的值*hstmt*。
