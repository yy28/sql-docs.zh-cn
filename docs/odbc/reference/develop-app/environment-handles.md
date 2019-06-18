---
title: 环境句柄 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a73ec4a842e220a16189f1390df167fe12bbab8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62942990"
---
# <a name="environment-handles"></a>环境句柄
*环境*是用来访问数据的全局上下文; 与环境关联是全局的性质，例如任何信息：  
  
-   环境的状态  
  
-   当前环境级别诊断  
  
-   连接在环境上当前分配的句柄  
  
-   每个环境属性的当前设置  
  
 在一段代码实现 ODBC （驱动程序管理器或驱动程序），环境句柄标识一种结构来包含此信息。  
  
 在 ODBC 应用程序中不常用环境句柄。 它们始终使用在调用**SQLDataSources**并**SQLDrivers**和有时用于调用**SQLAllocHandle**， **SQLEndTran**，**SQLFreeHandle**， **SQLGetDiagField**，并**SQLGetDiagRec**。  
  
 每个段实现 ODBC （驱动程序管理器或驱动程序） 的代码包含一个或多个环境句柄。 例如，驱动程序管理器维护每个应用程序连接到它的单独的环境句柄。 分配环境句柄**SQLAllocHandle**和与已释放**SQLFreeHandle**。
