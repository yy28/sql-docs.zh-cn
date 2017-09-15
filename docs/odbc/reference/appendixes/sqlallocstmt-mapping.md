---
title: "SQLAllocStmt 映射 |Microsoft 文档"
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
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8361f0b77e8f15f775eece7aae9b599be5e62ac
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

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
