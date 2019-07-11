---
title: SQLAllocStmt Mapping | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1139d87d9f97a3d63236c03e7cf4ced787ad8e85
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793551"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt 映射
当应用程序调用**SQLAllocStmt**通过 ODBC *3.x*驱动程序，将会调用：  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 映射到**SQLAllocHandle**由驱动程序管理器中的驱动程序，如下所示：  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 与*InputHandle*设置为*hdbc*并*OutputHandlePtr*设置为*phstmt*。
