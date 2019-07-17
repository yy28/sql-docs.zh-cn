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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107292"
---
# <a name="state-transitions"></a>状态转换
ODBC 定义离散*状态*为每个环境中，每个连接和每个语句。 例如，在环境有三个可能的状态：（在其中任何环境已分配） 的未分配，分配的 （在其中分配一个环境，但不分配任何连接） 和 （在其中一个环境和一个或多个连接都已分配） 的连接。 连接具有七个可能的状态;语句具有 13 可能的状态。  
  
 特定项，标识其句柄，将从一个状态到另一个时应用程序调用特定的函数，并将该句柄传递给该项目。 调用此类移动*状态切换*。 例如，分配环境句柄与**SQLAllocHandle**将环境从未分配移动到已分配，并释放与该句柄**SQLFreeHandle**返回从已分配到未分配。 ODBC 定义有限的数量的合法的状态转换，它是另一种说法： 必须以特定顺序调用函数。  
  
 一些函数，如**SQLGetConnectAttr**，根本不影响状态。 其他函数将影响单个项的状态。 例如， **SQLDisconnect**移动连接从连接状态为已分配的状态。 最后，某些功能会影响多个项的状态。 例如，分配连接句柄与**SQLAllocHandle**移动连接从未分配到已分配状态，并将环境从已分配移动到连接的状态。  
  
 如果应用程序调用不按顺序的函数，该函数将返回*状态转换错误*。 例如，如果环境处于连接状态和应用程序调用**SQLFreeHandle**与该环境句柄**SQLFreeHandle**返回 SQLSTATE HY010 （函数序列错误）因为只有在环境处于已分配状态时可调用它。 通过将定义此为状态转换无效，ODBC 阻止应用程序的活动连接时释放环境。  
  
 一些状态转换是 ODBC 的设计中固有的。 例如，不能以分配连接句柄，而第一个分配环境句柄，因为分配连接句柄的函数需要一个环境句柄。 其他状态转换会强制驱动程序管理器和驱动程序执行。 例如， **SQLExecute**执行已准备的语句。 如果语句句柄传递给它不是在准备就绪状态， **SQLExecute**返回 SQLSTATE HY010 （函数序列错误）。  
  
 从应用程序的角度来看，状态转换通常都很简单：合法的状态转换都趋向于手中手动编写良好的应用程序的流。 状态转换是驱动程序管理器和驱动程序变得更加复杂，因为它们必须跟踪的环境中，每个连接和每个语句的状态。 这项工作的大多数操作是由驱动程序管理器中;使用具有挂起结果的语句时出现的大部分必须由驱动程序完成工作。  
  
 此手册的部分 1 和 2 ("ODBC 简介"和"开发应用程序和驱动程序") 通常不应明确提及状态转换。 相反，它们描述必须调用函数的顺序。 例如，"执行的语句"状态必须与准备语句**SQLPrepare**可以通过执行之前**SQLExecute**。 有关完整的状态和状态转换，包括哪些转换将检查由驱动程序管理器和驱动程序，必须检查该说明请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
