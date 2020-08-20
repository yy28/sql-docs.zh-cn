---
description: 环境句柄
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461499"
---
# <a name="environment-handles"></a>环境句柄
*环境*是用于访问数据的全局上下文;与环境相关联的任何信息都是全局性的，例如：  
  
-   环境状态  
  
-   当前环境级别诊断  
  
-   当前在环境中分配的连接的句柄  
  
-   每个环境属性的当前设置  
  
 在 (驱动程序管理器或驱动程序) 实现 ODBC 的一段代码中，环境句柄标识了包含此信息的结构。  
  
 在 ODBC 应用程序中不经常使用环境句柄。 它们始终用于对 **SQLDataSources** 和 **SQLDrivers** 的调用，有时用于调用 **SQLAllocHandle**、 **SQLEndTran**、 **SQLFreeHandle**、 **SQLGetDiagField**和 **SQLGetDiagRec**。  
  
 实现 ODBC (驱动程序管理器或驱动程序) 的每个代码段都包含一个或多个环境句柄。 例如，驱动程序管理器为连接到它的每个应用程序维护单独的环境句柄。 环境句柄通过 **SQLAllocHandle** 分配，并与 **SQLFreeHandle**一起释放。
