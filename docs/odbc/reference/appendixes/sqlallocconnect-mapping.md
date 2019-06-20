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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bdb63e9610d00c0736f640b6f4c4d743f3335c7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280983"
---
# <a name="sqlallocconnect-mapping"></a>SQLAllocConnect 映射
当应用程序调用**SQLAllocConnect**通过 ODBC 3。*x*驱动程序，将会调用**SQLAllocConnect**(*henv*， *phdbc*) 映射到**SQLAllocHandle** ，如下所示：  
  
1.  驱动程序管理器分配一个连接，并将其返回给应用程序。  
  
2.  当应用程序建立的连接时，驱动程序管理器调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_DBC, InputHandle, OutputHandlePtr)  
    ```  
  
     使用驱动程序中*InputHandle*设置为*henv*，并*OutputHandlePtr*设置为*phdbc*。
