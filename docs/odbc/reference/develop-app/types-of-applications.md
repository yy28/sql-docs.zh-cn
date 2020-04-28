---
title: 应用程序的类型 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305528"
---
# <a name="types-of-applications"></a>应用程序类型
ODBC 应用程序可以按如下方式分类：  
  
-   **纯 ODBC 2。**  
     ** _x_应用程序**A 32 位应用程序：  
  
    -   仅调用 ODBC 2。*x*函数（包括 ODBC 1.0 函数**SQLSetParam**）。 其中包括 ODBC 1。*x*已移植到32位的应用程序。  
  
    -   应为 ODBC 2。*x*行为更改的功能。 （有关详细信息，请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。）  
  
    -   尚未重新编译 ODBC 3.5 标头。  
  
-   **纯 ODBC 2。**  
     **_x_重新编译**了纯 ODBC 2 的应用程序。已使用 ODBC 3.5 头文件重新编译的*x*应用程序，设置 ODBCVER = 0x0250。  
  
-   **纯 ODBC 2。**  
     **_x_ Unicode 应用程序**是纯 ODBC 2。*x*重新编译了 Unicode 兼容的应用程序，并使用 SQL_WCHAR 数据类型。  
  
-   **纯开放式组和符合 ISO**-的**ODBC 应用程序**A 32 位应用程序：  
  
    -   调用在开放组或 ISO CLI 标准中定义的函数。 （这些函数可能包括弃用的3.0 函数。）  
  
    -   不使用 Unicode 数据类型。  
  
    -   对于具有行为更改的功能，应使用 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.0 应用程序**32位应用程序：  
  
    -   已编译为3.0 标头。  
  
    -   调用任何 ODBC 3.0 函数，其中可能包括已弃用的函数。  
  
    -   对于具有行为更改的功能，应使用 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.5 应用程序**32或64位应用程序：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.5 函数，其中可能包括已弃用的函数。  
  
    -   对于具有行为更改的功能，应使用 ODBC 3.5 行为。  
  
-   **纯 ODBC 3.8 （或更高版本）应用程序**32位或64位应用程序：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.8 函数，其中可能包括已弃用的函数。  
  
    -   对于具有行为更改的功能，应使用 ODBC 3.8 行为。  
  
-   **已替换应用程序**32或64位应用程序：  
  
    -   实现重复功能的新行为。  
  
    -   仅在条件代码中使用更高版本的 ODBC 中的任何新功能。  
  
    -   具有有限的条件代码来处理行为更改或已将自身注册为 ODBC 应用程序的早期版本。
