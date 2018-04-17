---
title: SQLAllocStmt 映射 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 936e7861da5aaccc9c5ca9c649524484640f5fb4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 映射
在应用程序调用**SQLAllocStmt**到 ODBC 3*.x*驱动程序，将会调用：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 映射到**SQLAllocHandle**由驱动程序管理器中的驱动程序，如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 与*InputHandle*设置为*hdbc*和*OutputHandlePtr*设置为*phstmt*。
