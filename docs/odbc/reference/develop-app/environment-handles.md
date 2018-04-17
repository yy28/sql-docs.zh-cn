---
title: 环境句柄 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffbc2ed4c1c496833237c3bda6d6e2c306a50cac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="environment-handles"></a>环境句柄
*环境*是用于访问数据的全局上下文; 与环境相关是任何信息，全局本质，如：  
  
-   环境的状态  
  
-   当前环境级诊断  
  
-   连接在环境上当前分配的句柄  
  
-   每个环境属性的当前设置  
  
 中的实现 ODBC （驱动程序管理器或驱动程序） 的代码段，环境句柄标识一个结构，用于包含此信息。  
  
 ODBC 应用程序中不常用环境句柄。 始终用在调用**SQLDataSources**和**SQLDrivers**和有时用于调用**SQLAllocHandle**， **SQLEndTran**，**SQLFreeHandle**， **SQLGetDiagField**，和**SQLGetDiagRec**。  
  
 每个段实现 ODBC （驱动程序管理器或驱动程序） 的代码包含一个或多个环境句柄。 例如，驱动程序管理器维护每个应用程序连接到它的单独的环境句柄。 环境句柄分配与**SQLAllocHandle**并释放与**SQLFreeHandle**。
