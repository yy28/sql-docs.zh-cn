---
title: SQLFreeStmt 映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77392dff0f22fcabd26b54cad700bb5cebcde2bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 映射
在应用程序调用**SQLFreeStmt**与*选项*参数通过 ODBC 3 SQL_DROP *.x*驱动程序，将会调用  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 与*处理*参数设置中的值为*hstmt*。
