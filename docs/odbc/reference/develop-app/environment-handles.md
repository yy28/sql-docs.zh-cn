---
title: 环境句柄 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300437"
---
# <a name="environment-handles"></a>环境句柄
*环境*是访问数据的全局上下文;与环境关联的是任何全局性信息，例如：  
  
-   环境的状态  
  
-   当前环境级诊断  
  
-   当前在环境中分配的连接的句柄  
  
-   每个环境属性的当前设置  
  
 在实现 ODBC（驱动程序管理器或驱动程序）的代码段中，环境句柄标识结构以包含此信息。  
  
 环境句柄在 ODBC 应用中不经常使用。 它们始终用于对**SQLDataSources**和**SQLDrivers 的**调用，有时用于对 SQLAllocHandle、SQLEndTran、SQLFreeHandle、SQLGetDiagField 和**SQLGetDiagRec**的调用。 **SQLAllocHandle** **SQLEndTran** **SQLFreeHandle** **SQLGetDiagField**  
  
 实现 ODBC 的每个代码段（驱动程序管理器或驱动程序）包含一个或多个环境句柄。 例如，驱动程序管理器为连接到它的每个应用程序维护一个单独的环境句柄。 环境句柄使用**SQLAllocHandle**分配，并释放**SQLFreeHandle**。
