---
title: 状态转换 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2512d277980b071523cfea6cbe132f2a3861b7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107292"
---
# <a name="state-transitions"></a>状态转换
ODBC 定义每个环境、每个连接和每个语句的离散*状态*。 例如，环境具有三种可能的状态： "未分配" （未分配环境）、"已分配" （在其中分配了环境但未分配任何连接）和 "连接" （其中，环境和一个或多个连接是已分配）。 连接有七种可能的状态;语句具有13个可能的状态。  
  
 当应用程序调用某个函数或函数并将句柄传递给该项时，由其句柄标识的特定项从一个状态移到另一个状态。 此类移动称为*状态转换*。 例如，使用**SQLAllocHandle**分配环境句柄会将环境从 "未分配" 移动到 "已分配"，并使用**SQLFreeHandle**释放该句柄，以将其从分配给 "未分配"。 ODBC 定义了有限数量的合法状态转换，这是另一种表示必须按特定顺序调用函数的方式。  
  
 某些函数（如**SQLGetConnectAttr**）不会影响状态。 其他函数会影响单个项的状态。 例如， **SQLDisconnect**将连接状态从连接状态移动到已分配状态。 最后，某些函数会影响多个项的状态。 例如，使用**SQLAllocHandle**分配连接句柄会将连接从未分配状态移动到已分配状态，并将环境从已分配的移动到连接状态。  
  
 如果应用程序按顺序调用函数，该函数将返回*状态转换错误*。 例如，如果环境处于连接状态，并且应用程序使用该环境句柄调用**SQLFreeHandle** ，则**SQLFREEHANDLE**将返回 SQLSTATE HY010 （函数序列错误），因为它只能在环境处于已分配状态时调用。 通过将此定义为无效的状态转换，ODBC 可防止应用程序在存在活动连接时释放环境。  
  
 某些状态转换在 ODBC 设计中是固有的。 例如，如果不先分配环境句柄，就无法分配连接句柄，因为分配连接句柄的函数需要环境句柄。 其他状态转换由驱动程序管理器和驱动程序强制执行。 例如， **SQLExecute**执行预定义语句。 如果传递给它的语句句柄未处于已准备状态，则**SQLExecute**将返回 SQLSTATE HY010 （函数序列错误）。  
  
 从应用程序的角度来看，状态转换通常是非常简单的：法律状态转换倾向于在编写良好的应用程序的流时使用。 状态转换对于驱动程序管理器和驱动程序更复杂，因为它们必须跟踪环境、每个连接和每个语句的状态。 此工作的大部分工作由驱动程序管理器执行;驱动程序必须完成的大部分工作都是通过包含挂起结果的语句来完成的。  
  
 本手册的第1和第2部分（"ODBC 简介" 和 "开发应用程序和驱动程序"）往往不显式提及状态转换。 相反，它们描述了必须调用函数的顺序。 例如，"执行语句" 表明必须先使用**SQLPrepare**准备语句，然后才能使用**SQLExecute**来执行。 有关状态和状态转换的完整说明，包括驱动程序管理器检查哪些转换以及哪些转换必须由驱动程序检查，请参阅[附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
