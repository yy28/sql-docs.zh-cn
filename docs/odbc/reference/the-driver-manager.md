---
title: "驱动程序管理器 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c66acd08644176170c56700720a438aa8ffcdb1b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="the-driver-manager"></a>驱动程序管理器
*驱动程序管理器*是一个库，管理应用程序和驱动程序之间的通信。 例如，在 Microsoft® Windows® 平台驱动程序管理器是动态链接库 (DLL) 由 Microsoft 编写并可以由用户的可再发行组件的 MDAC 2.8 SP1 sdk 一起重新分发。  
  
 驱动程序管理器主要作为一种便于使用应用程序编写器存在而且可解决许多问题普遍适用于所有应用程序。 其中包括确定要加载的驱动程序基于数据源名称、 加载和卸载驱动程序，以及驱动程序中调用函数。  
  
 若要查看为什么后者是问题，请考虑会发生什么情况如果应用程序驱动程序中调用函数直接。 除非应用程序已直接链接到特定的驱动程序，则必须先生成指向该驱动程序中的函数的指针的表并通过指针调用这些函数。 一次为多个驱动程序使用相同的代码将添加另一个级别的复杂性。 应用程序将首先需要设置以指向正确的驱动程序，在正确的函数的函数指针，然后调用通过该指针的函数。  
  
 驱动程序管理器提供单个位置调用每个函数，从而解决了此问题。 应用程序链接到在驱动程序管理器中的驱动程序管理器和调用 ODBC 函数不是驱动程序。 应用程序标识目标驱动程序和数据源与*连接句柄*。 当它将加载驱动程序时，驱动程序管理器将生成指向该驱动程序中的函数的指针的表。 它由应用程序传递的连接句柄用于在目标驱动程序中查找函数的地址，并按地址调用该函数。  
  
 大多数情况下，驱动程序管理器仅传递到正确的驱动程序应用程序的函数调用。 但是，它还实现一些函数 (**SQLDataSources**， **SQLDrivers**，和**SQLGetFunctions**) 并执行基本的错误检查。 例如，驱动程序管理器检查句柄不是 null 指针，函数称为按正确的顺序，并且某些函数自变量有效。 检查由驱动程序管理器中的错误的完整说明，请参阅每个函数的参考部分和[附录 b: ODBC 状态转换表](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 最终的主要角色的驱动程序管理器是加载和卸载驱动程序。 应用程序加载和卸载仅驱动程序管理器。 当它想要使用的特定驱动程序时，它将调用连接函数 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 驱动程序管理器中，并指定特定数据源或驱动程序，如"记帐"或"SQL Server。"的名称 使用此名称，驱动程序管理器搜索驱动程序的文件名称，例如 Sqlsrvr.dll 的数据源信息。 然后将加载驱动程序 （假设未加载）、 将每个函数的地址存储在驱动程序，并调用中的驱动程序，然后初始化自身并连接到数据源的连接函数。  
  
 完成应用程序时使用驱动程序，它将调用**SQLDisconnect**驱动程序管理器中。 驱动程序管理器驱动程序，从数据源断开连接中调用此函数。 但是，驱动程序管理器驱动程序在内存中保留以防应用程序重新连接到它。 仅当应用程序释放该驱动程序使用的连接或将连接用于不同驱动程序，并且任何其他连接使用的驱动程序时，它会卸载该驱动程序。 在加载和卸载驱动程序的驱动程序管理器角色的完整说明，请参阅[连接过程中的驱动程序管理器角色](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。
