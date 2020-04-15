---
title: SQLAllocStmt 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 447233a3ba014a5ef92f2f49840ad302f8aeccf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305480"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLAllocStmt**时，调用：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 驱动程序中的驱动程序管理器映射到**SQLAllocHandle，** 如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 与*输入句柄*设置为*hdbc*和*输出句柄Ptr*设置为*phstmt*。
