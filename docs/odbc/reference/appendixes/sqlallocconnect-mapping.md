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
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a699be0e0c93ea48646375c0f6d9c0ab55ba74a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 映射
在应用程序调用**SQLAllocConnect**到 ODBC 3。*x*驱动程序，将会调用**SQLAllocConnect**(*henv*， *phdbc*) 映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配连接，并将其返回给应用程序。  
  
2.  当应用程序建立的连接时，驱动程序管理器将调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     与驱动程序中*InputHandle*设置为*henv*，和*OutputHandlePtr*设置为*phdbc*。
