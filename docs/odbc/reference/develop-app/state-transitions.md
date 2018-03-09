---
title: "状态转换 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6795a0e730f1b927b7921863714a2a9db55551e4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="state-transitions"></a>状态转换
ODBC 定义离散*状态*为每个环境，每个连接和每个语句。 例如，环境有三个可能的状态： 未分配的 （中都没有环境将分配），已分配 （在其中分配环境，但没有连接被分配） 和连接 （在其环境和一个或多个连接都是已分配）。 连接具有七个可能的状态;语句具有 13 可能的状态。  
  
 一个特定的项，标识由其句柄，从一个状态到另一个时移动应用程序调用某函数，并将该句柄传递给该项目。 调用此类移动*状态切换*。 例如，分配环境句柄与**SQLAllocHandle**将从未分配的环境移动到已分配，并释放与该句柄**SQLFreeHandle**返回从已分配到未分配。 ODBC 定义有限的数量的合法状态转换，它是另一种说法必须以特定顺序调用函数的方法。  
  
 一些函数，如**SQLGetConnectAttr**，根本不影响状态。 其他函数影响单个项的状态。 例如， **SQLDisconnect**将连接从连接状态更改为已分配状态。 最后，某些功能会影响多个项的状态。 例如，分配连接句柄与**SQLAllocHandle**将连接从未分配移到已分配状态，并且将从已分配的环境移动到连接的状态。  
  
 如果应用程序调用顺序的函数，该函数将返回*状态转换错误*。 例如，如果环境处于连接状态和应用程序调用**SQLFreeHandle**具有该环境句柄， **SQLFreeHandle**返回 SQLSTATE HY010 （函数序列错误）因为仅当环境处于已分配状态时，才可调用它。 通过定义这与无效状态转换，ODBC 阻止应用程序活动连接时释放环境。  
  
 某些状态转换是 ODBC 的设计中固有的。 例如，不可能无需分配环境句柄，第一个分配连接句柄，因为分配连接句柄的函数需要一个环境句柄。 其他状态转换会强制执行由驱动程序管理器和驱动程序。 例如， **SQLExecute**执行已准备的语句。 如果语句句柄传递给它未处于已准备状态， **SQLExecute**返回 SQLSTATE HY010 （函数序列错误）。  
  
 从应用程序的角度来看，状态转换通常都很简单： 合法状态转换都趋向于手中手工编写良好的应用程序流使用。 状态转换是驱动程序管理器和驱动程序变得更加复杂，因为它们必须跟踪的环境、 每个连接和每个语句的状态。 大部分此工作完成了通过驱动程序管理器中;使用具有挂起结果的语句时出现的大部分工作，必须由驱动程序来完成。  
  
 此手册 1 和 2 部分 ("ODBC 简介"和"开发应用程序和驱动程序") 往往不显式指出状态转换。 相反，这些主题描述必须调用函数的顺序。 例如，"执行的语句"状态，必须使用准备语句**SQLPrepare**可以通过执行之前**SQLExecute**。 完整描述的状态和状态转换，包括的转换会检查由驱动程序管理器，其必须检查由驱动程序，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
