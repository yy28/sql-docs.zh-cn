---
title: SQLAllocEnv 映射 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304038"
---
# <a name="sqlallocenv-mapping"></a>SQLAllocEnv 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLAllocEnv**时，对**SQLAllocEnv***（phenv*） 的调用将映射到**SQLAllocHandle，** 如下所示：  
  
1.  驱动程序管理器分配一个环境句柄并将其返回到应用程序。 驱动程序管理器调用**SQLSetEnvAttr**将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC2。  
  
2.  当应用程序建立与驱动程序的第一个连接时，驱动程序管理器调用  
  
    ```  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, OutputHandlePtr)  
    ```  
  
     在具有*OutputHandlePtr*设置为*phenv*的驱动程序中。
