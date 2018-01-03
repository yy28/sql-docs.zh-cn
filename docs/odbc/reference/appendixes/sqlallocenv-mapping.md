---
title: "SQLAllocEnv 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34c2c0b63437da93770cdd1b6ed38bf3dbb4211f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 映射
在应用程序调用**SQLAllocEnv**到 ODBC 3*.x*驱动程序，将会调用**SQLAllocEnv**(*phenv*) 映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配的环境句柄，并将其返回给应用程序。 驱动程序管理器调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC2。  
  
2.  当应用程序建立第一个连接到的驱动程序时，驱动程序管理器将调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     与驱动程序中*OutputHandlePtr*设置为*phenv*。
