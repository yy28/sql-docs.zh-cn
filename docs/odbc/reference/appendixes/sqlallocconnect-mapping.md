---
title: SQLAllocConnect 映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLAllocConnect
ms.assetid: ac89dd1f-c565-47cc-8fa3-6fa5f80b5d63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1f2485112213bb3b4168bc72f96cee353cd1101
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 映射
在应用程序调用**SQLAllocConnect**到 ODBC 3。*x*驱动程序，将会调用**SQLAllocConnect**(*henv*， *phdbc*) 映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配连接，并将其返回给应用程序。  
  
2.  当应用程序建立的连接时，驱动程序管理器将调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     与驱动程序中*InputHandle*设置为*henv*，和*OutputHandlePtr*设置为*phdbc*。
