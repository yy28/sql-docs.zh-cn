---
title: SQLAllocStmt 映射 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305480"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 映射
当应用程序*通过 ODBC 1.x*驱动程序调用**SQLAllocStmt**时，将调用：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 驱动程序管理器将按如下所示映射到**SQLAllocHandle** ：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 将*将 inputhandle*设置为*hdbc* ，并将*OutputHandlePtr*设置为*phstmt*。
