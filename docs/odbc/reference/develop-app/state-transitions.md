---
title: 状态转换 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a480b7ff8953ef94f0efc4886a09731730a61b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299690"
---
# <a name="state-transitions"></a>状态转换
ODBC 为每个环境、每个连接和每个语句定义离散*状态*。 例如，环境有三种可能状态：未分配（其中未分配环境）、已分配（其中分配了环境但未分配连接）和连接（其中分配了环境和一个或多个连接）。 连接有七种可能状态;语句有 13 种可能状态。  
  
 当应用程序调用某个函数或函数并将句柄传递给该项时，由其句柄标识的特定项从一种状态移动到另一个状态。 这种运动被称为*国家过渡*。 例如，使用**SQLAllocHandle**分配环境句柄会将环境从"未分配"移动到"已分配"，并且释放使用**SQLFreeHandle**的句柄将环境从"已分配"返回到"未分配"。 ODBC 定义了数量有限的法律状态转换，这是另一种说法，即必须按特定顺序调用函数。  
  
 某些函数（如**SQLGetConnectAttr）** 根本不影响状态。 其他函数会影响单个项的状态。 例如 **，SQLDisconnect**将连接从连接状态移动到已分配状态。 最后，某些函数会影响多个项的状态。 例如，使用**SQLAllocHandle**分配连接句柄会将连接从未分配移动到已分配状态，并将环境从"已分配"状态移动到连接状态。  
  
 如果应用程序按顺序调用函数，则函数将返回*状态转换错误*。 例如，如果环境处于连接状态，并且应用程序使用该环境句柄调用**SQLFreeHandle，SQLFreeHandle**将返回 SQLSTATE HY010（函数序列错误），因为只有在环境处于已分配状态时才能调用它。 **SQLFreeHandle** 通过将此定义为无效状态转换，ODBC 可防止应用程序在有活动连接时释放环境。  
  
 一些状态转换是 ODBC 设计中固有的。 例如，如果不首先分配环境句柄，就无法分配连接句柄，因为分配连接句柄的函数需要环境句柄。 其他状态转换由驱动程序管理器和驱动程序强制执行。 例如 **，SQLExecute**执行准备好的语句。 如果传递给它的语句句柄未处于准备状态 **，SQLExecute**将返回 SQLSTATE HY010（函数序列错误）。  
  
 从应用程序的角度来看，状态转换通常很简单：法律状态转换往往与编写良好的应用程序流齐头并进。 状态转换对于驱动程序管理器和驱动程序来说更为复杂，因为它们必须跟踪环境、每个连接和每个语句的状态。 大部分工作由驾驶员经理完成;驱动程序必须完成的大部分工作都使用具有挂起结果的语句进行。  
  
 本手册的第 1 部分和第 2 部分（"ODBC 简介"和"开发应用程序和驱动程序"）往往没有明确提及状态转换。 相反，它们描述必须调用函数的顺序。 例如，"执行语句"指出，必须先使用**SQLPrepare 编写**语句，然后才能使用**SQLExecute**执行语句。 有关状态和状态转换的完整说明，包括驱动程序管理器检查哪些转换，哪些转换必须由驱动程序检查，请参阅[附录 B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
