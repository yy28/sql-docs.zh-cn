---
title: 驱动程序管理器 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 686a2b9673fb392f969a42f4cc86dd95a95668a6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286791"
---
# <a name="the-driver-manager"></a>驱动程序管理器
*驱动程序管理器*是用于管理应用程序和驱动程序之间的通信的库。 例如，在 Microsoft® Windows®平台上，驱动程序管理器是一个动态链接库（DLL），由 Microsoft 编写，可再发行的 MDAC 2.8 SP1 SDK 的用户可以重新分发。  
  
 驱动程序管理器的存在主要是为应用程序编写器提供便利，并解决了所有应用程序通用的一些问题。 其中包括根据数据源名称确定要加载的驱动程序、加载和卸载驱动程序以及在驱动程序中调用函数。  
  
 若要查看后一种问题的原因，请考虑应用程序在驱动程序中直接调用函数会发生什么情况。 除非应用程序直接链接到特定的驱动程序，否则它必须生成一个指向该驱动程序中的函数的指针表，并通过指针调用这些函数。 如果一次对多个驱动程序使用相同的代码，则可能会增加复杂程度。 应用程序首先必须将函数指针设置为指向正确的驱动程序中的正确函数，然后通过该指针调用函数。  
  
 驱动程序管理器通过提供一个用于调用每个函数的位置来解决此问题。 应用程序链接到驱动程序管理器，并在驱动程序管理器中调用 ODBC 函数，而不是驱动程序。 应用程序使用*连接句柄*标识目标驱动程序和数据源。 加载驱动程序时，驱动程序管理器将生成一个指向该驱动程序中的函数的指针表。 它使用应用程序传递的连接句柄来查找目标驱动程序中的函数地址，并按地址调用该函数。  
  
 大多数情况下，驱动程序管理器只是将函数调用从应用程序传递到正确的驱动程序。 但是，它还实现了一些函数（**SQLDataSources**、 **SQLDrivers**和**SQLGetFunctions**），并执行了基本的错误检查。 例如，驱动程序管理器检查处理不是 null 指针，函数按正确的顺序调用，并且某些函数参数是有效的。 有关驱动程序管理器检查的错误的完整说明，请参阅每个函数的参考部分和[附录 B： ODBC 状态转换表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 驱动程序管理器的最终主要角色是加载和卸载驱动程序。 应用程序仅加载并卸载驱动程序管理器。 当它要使用特定的驱动程序时，它将在驱动程序管理器中调用连接函数（**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**），并指定特定数据源或驱动程序的名称，例如 "会计" 或 "SQL Server"。 使用此名称，驱动程序管理器会在数据源信息中搜索驱动程序的文件名，例如 Sqlsrvr。 然后加载驱动程序（假定尚未加载），将每个函数的地址存储在驱动程序中，并在驱动程序中调用连接函数，然后该驱动程序将初始化自身并连接到数据源。  
  
 使用驱动程序完成应用程序后，它将在驱动程序管理器中调用**SQLDisconnect** 。 驱动程序管理器将在与数据源断开连接的驱动程序中调用此函数。 但是，当应用程序重新连接到内存中时，驱动程序管理器会将驱动程序保留在内存中。 仅当应用程序释放驱动程序使用的连接或将连接用于不同的驱动程序，且没有其他连接使用驱动程序时，它才会卸载该驱动程序。 有关加载和卸载驱动程序的驱动程序管理器角色的完整说明，请参阅[连接过程中的驱动程序管理器的角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
