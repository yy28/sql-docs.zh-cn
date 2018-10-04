---
title: 类型的应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e46075e55aa14784e967b3620de5855a47c4bd6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676615"
---
# <a name="types-of-applications"></a>应用程序类型
ODBC 应用程序可以进行分类，如下所示：  
  
-   **纯 ODBC 2。**  
     ***x*应用程序**的 32 位应用程序的：  
  
    -   调用仅 ODBC 2。*x*函数 (包括 ODBC 1.0 函数**SQLSetParam**)。 这包括 ODBC 1。*x*已经移植到 32 位的应用程序。  
  
    -   需要 ODBC 2。*x*有行为的更改的功能的行为。 (请参阅[行为的更改](../../../odbc/reference/develop-app/behavioral-changes.md)有关详细信息。)  
  
    -   已不被重新编译使用 ODBC 3.5 标头。  
  
-   **纯 ODBC 2。**  
     ***x*重新编译应用程序**纯 ODBC 2。*x*已被重新编译使用 ODBC 3.5 标头文件的应用程序通过设置 ODBCVER = 0x0250。  
  
-   **纯 ODBC 2。**  
     ***x* Unicode 应用程序**纯 ODBC 2。*x*重新编译应用程序符合 Unicode 的并使用 SQL_WCHAR 数据类型。  
  
-   **纯打开组和 ISO**–**符合 ODBC 应用程序的**的 32 位应用程序的：  
  
    -   调用 Open Group 或 ISO CLI 标准中定义的函数。 （这些函数可能包括不推荐使用 3.0 函数）。  
  
    -   不使用 Unicode 数据类型。  
  
    -   需要有行为的更改的功能的 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.0 应用程序**的 32 位应用程序的：  
  
    -   编译使用 3.0 标头。  
  
    -   调用任何 ODBC 3.0 函数时，可能包括那些已弃用。  
  
    -   需要有行为的更改的功能的 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.5 应用程序**32 位还是 64 位应用程序的：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.5 函数时，可能包括那些已弃用。  
  
    -   需要有行为的更改的功能的 ODBC 3.5 行为。  
  
-   **纯 ODBC 3.8 （或更高版本） 应用程序**的 32 位或 64 位应用程序的：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.8 函数时，可能包括那些已弃用。  
  
    -   需要 ODBC 3.8 已具有的行为更改的功能的行为。  
  
-   **替换为应用程序**32 位还是 64 位应用程序的：  
  
    -   实现重复的功能的新行为。  
  
    -   仅在条件代码中更高版本的 ODBC 版本中使用的任何新功能。  
  
    -   具有有限的条件代码来处理行为的更改或已将自己为早期版本的 ODBC 应用程序注册。
