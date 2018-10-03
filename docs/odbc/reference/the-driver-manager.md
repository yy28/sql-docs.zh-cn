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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c1ae3f098aea3886d5cb84a0bfcb7553a8181fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47791547"
---
# <a name="the-driver-manager"></a>驱动程序管理器
*驱动程序管理器*是管理应用程序和驱动程序之间的通信的库。 例如，在 Microsoft® Windows® 平台上驱动程序管理器是由 Microsoft 编写，可以重新分发的可再发行组件的 MDAC 2.8 SP1 SDK 用户的动态链接库 (DLL)。  
  
 驱动程序管理器存在主要是为了方便应用程序编写器，可解决许多问题普遍适用于所有应用程序。 其中包括确定要加载的驱动程序基于数据源名称、 加载和卸载驱动程序，以及驱动程序中调用函数。  
  
 若要查看为什么后者是一个问题，请考虑会发生什么情况如果应用程序在驱动程序中调用函数直接。 除非应用程序直接链接到的特定驱动程序，它必须生成指向该驱动程序中的函数的指针的表和调用这些函数的指针。 一次为多个驱动程序使用相同的代码将添加另一个级别的复杂性。 应用程序将首先必须设置为指向正确的驱动程序，在正确的函数的函数指针，然后调用通过该指针的函数。  
  
 驱动程序管理器通过提供一个单一位置来调用每个函数来解决此问题。 应用程序链接到驱动程序管理器并调用 ODBC 函数在驱动程序管理器中，不是驱动程序。 应用程序标识与目标驱动程序和数据源*连接句柄*。 当它加载驱动程序时，驱动程序管理器将生成指向该驱动程序中的函数的指针的表。 它由应用程序传递的连接句柄用于在目标驱动程序中查找的函数地址，并调用该函数的地址。  
  
 大多数情况下，驱动程序管理器只需将传递到正确的驱动程序应用程序的函数调用。 但是，它还实现一些函数 (**SQLDataSources**， **SQLDrivers**，并**SQLGetFunctions**) 并执行基本的错误检查。 例如，驱动程序管理器检查句柄不是空指针，以正确的顺序，调用的函数和某些函数自变量都有效。 检查由驱动程序管理器中的错误的完整说明，请参阅每个函数的参考部分和[附录 b: ODBC 状态转换表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 驱动程序管理器中的最后一个主要角色是加载和卸载驱动程序。 应用程序加载和卸载该驱动程序管理器。 当它想要使用的特定驱动程序时，它将调用连接函数 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 驱动程序管理器中，并指定特定数据源或驱动程序，例如"财务"或"SQL Server。"的名称 使用此名称，驱动程序管理器中搜索驱动程序的文件名称，例如 Sqlsrvr.dll 的数据源信息。 然后加载驱动程序 （假设未加载），将每个函数的地址存储在驱动程序，并调用中的驱动程序，然后初始化自身并连接到数据源的连接函数。  
  
 完成应用程序时使用的驱动程序，它会调用**SQLDisconnect**驱动程序管理器中。 驱动程序管理器中的驱动程序，与数据源断开连接调用此函数。 但是，驱动程序管理器驱动程序在内存中保留在应用程序重新连接到它的情况下。 仅当释放该驱动程序使用的连接或不同驱动程序，则使用该连接的应用程序和任何其他连接使用的驱动程序时，它会卸载该驱动程序。 有关驱动程序管理器中加载和卸载驱动程序的角色的完整说明，请参阅[的连接过程中的驱动程序管理器角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
