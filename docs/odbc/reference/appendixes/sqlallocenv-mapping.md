---
title: SQLAllocEnv Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 841310d1e51084ae6a61c629b8782a8b84c665f8
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793584"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 映射
当应用程序调用**SQLAllocEnv**通过 ODBC *3.x*驱动程序，将会调用**SQLAllocEnv**(*phenv*) 映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配环境句柄，并将其返回给应用程序。 驱动程序管理器调用**SQLSetEnvAttr**将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC2。  
  
2.  当应用程序建立到驱动程序的第一个连接时，驱动程序管理器调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     使用驱动程序中*OutputHandlePtr*设置为*phenv*。
