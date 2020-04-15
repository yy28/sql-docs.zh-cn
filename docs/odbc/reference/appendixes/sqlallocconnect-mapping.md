---
title: SQLAlloc连接映射 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305518"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 映射
当应用程序通过 ODBC 3 调用**SQLAllocConnect**时。*x*驱动程序，对**SQLAllocConnect**的调用 *（henv，* *phdbc*） 映射到**SQLAllocHandle，** 如下所示：  
  
1.  驱动程序管理器分配连接并将其返回到应用程序。  
  
2.  当应用程序建立连接时，驱动程序管理器调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     在驱动程序与*输入句柄*设置为*henv，* 和*输出句柄Ptr*设置为*phdbc*。
