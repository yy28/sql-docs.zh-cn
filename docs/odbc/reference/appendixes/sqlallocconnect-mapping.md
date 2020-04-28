---
title: SQLAllocConnect 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25e72cd3830cea8504983f4348f6c200261490f4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305518"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 映射
当应用程序通过 ODBC 3 调用**SQLAllocConnect**时。*x*驱动程序、对**SQLAllocConnect**（*henv*、 *phdbc*）的调用映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配一个连接，并将其返回给应用程序。  
  
2.  当应用程序建立连接时，驱动程序管理器会调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在 "*将 inputhandle* " 设置为 " *henv*" 的驱动程序中，将*OutputHandlePtr*设置为 " *phdbc*"。
