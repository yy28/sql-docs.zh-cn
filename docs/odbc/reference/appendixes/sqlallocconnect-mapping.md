---
title: "SQLAllocConnect 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0188c47d6abfd294dc1a9c20c04ea7d271443a18
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 映射
在应用程序调用**SQLAllocConnect**到 ODBC 3。*x*驱动程序，将会调用**SQLAllocConnect**(*henv*， *phdbc*) 映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配连接，并将其返回给应用程序。  
  
2.  当应用程序建立的连接时，驱动程序管理器将调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     与驱动程序中*InputHandle*设置为*henv*，和*OutputHandlePtr*设置为*phdbc*。

