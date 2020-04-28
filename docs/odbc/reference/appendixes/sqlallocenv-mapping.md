---
title: SQLAllocEnv 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocEnv
ms.assetid: 4bb51845-ee91-4b97-9dd4-2fab977f2aec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb26e3443fabda2d6490c071b1f2668895e66b8d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304038"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 映射
当应用程序*通过 ODBC 1.x*驱动程序调用**SQLAllocEnv**时，对**SQLAllocEnv**（*phenv*）的调用映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配环境句柄并将其返回给应用程序。 驱动程序管理器调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC2。  
  
2.  当应用程序建立与驱动程序的第一个连接时，驱动程序管理器会调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     在 " *OutputHandlePtr* " 设置为 " *phenv*" 的驱动程序中。
