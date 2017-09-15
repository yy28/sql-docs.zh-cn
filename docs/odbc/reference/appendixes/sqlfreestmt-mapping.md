---
title: "SQLFreeStmt 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: df3cfba17f19074fbe00f33ef7fba098a4fe8184
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-mapping"></a>SQLFreeStmt 映射
在应用程序调用**SQLFreeStmt**与*选项*参数通过 ODBC 3 SQL_DROP*.x*驱动程序，将会调用  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 与*处理*参数设置中的值为*hstmt*。
