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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf79d3ef813e87e785cea588cfc1d6e3eed44ee4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064994"
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
