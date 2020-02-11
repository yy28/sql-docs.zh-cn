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
ms.openlocfilehash: 409b2c14282238766457d349287f65d90fe463b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114322"
---
# <a name="environment-handles"></a>环境句柄
*环境*是用于访问数据的全局上下文;与环境相关联的任何信息都是全局性的，例如：  
  
-   环境状态  
  
-   当前环境级别诊断  
  
-   当前在环境中分配的连接的句柄  
  
-   每个环境属性的当前设置  
  
 在实现 ODBC （驱动程序管理器或驱动程序）的代码段中，环境句柄标识包含此信息的结构。  
  
 在 ODBC 应用程序中不经常使用环境句柄。 它们始终用于对**SQLDataSources**和**SQLDrivers**的调用，有时用于调用**SQLAllocHandle**、 **SQLEndTran**、 **SQLFreeHandle**、 **SQLGetDiagField**和**SQLGetDiagRec**。  
  
 实现 ODBC 的每个代码段（驱动程序管理器或驱动程序）都包含一个或多个环境句柄。 例如，驱动程序管理器为连接到它的每个应用程序维护单独的环境句柄。 环境句柄通过**SQLAllocHandle**分配，并与**SQLFreeHandle**一起释放。
