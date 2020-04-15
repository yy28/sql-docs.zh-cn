---
title: 应用程序类型 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305528"
---
# <a name="types-of-applications"></a>应用程序类型
ODBC 应用程序可分类如下：  
  
-   **纯 ODBC 2.**  
     ** _x_应用程序**A 32 位应用程序， ：  
  
    -   仅调用 ODBC 2。*x*函数（包括 ODBC 1.0 函数**SQLSetParam**）。 其中包括 ODBC 1。*已*移植到 32 位的 x 应用程序。  
  
    -   预期 ODBC 2.*具有*行为更改的功能的 x 行为。 （有关详细信息，请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
    -   尚未使用 ODBC 3.5 标头重新编译。  
  
-   **纯 ODBC 2.**  
     **_x_重新编译应用程序**纯 ODBC 2。*x*使用 ODBC 3.5 标头文件重新编译的应用程序，通过设置 ODBCVER=0x0250。  
  
-   **纯 ODBC 2.**  
     **_x_ Unicode 应用程序**纯 ODBC 2。*x*重新编译的应用程序符合 Unicode，并使用SQL_WCHAR数据类型。  
  
-   **纯开放组和符合 ISO**-**标准的 ODBC 应用程序**A 32 位应用程序，它：  
  
    -   在开放组或 ISO CLI 标准中定义的调用函数。 （这些函数可能包括弃用的 3.0 函数。  
  
    -   不使用 Unicode 数据类型。  
  
    -   对于行为更改的要素，预期 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.0 应用**32 位应用程序，它：  
  
    -   使用 3.0 标头编译。  
  
    -   调用任何 ODBC 3.0 函数，可能包括已弃用的功能。  
  
    -   对于行为更改的要素，预期 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.5 应用**32 位或 64 位应用程序，它：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.5 函数，可能包括已弃用的功能。  
  
    -   对于行为更改的要素，预期 ODBC 3.5 行为。  
  
-   **纯 ODBC 3.8（或更高版本）应用**32 位或 64 位应用程序，它：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.8 函数，可能包括已弃用的功能。  
  
    -   对于行为更改的要素，预期 ODBC 3.8 行为。  
  
-   **替换应用程序**32 位或 64 位应用程序，它：  
  
    -   为重复的功能实现新行为。  
  
    -   仅在条件代码中使用更高版本的 ODBC 中的任何新功能。  
  
    -   具有用于处理行为更改的条件代码有限，或已注册为 ODBC 应用程序的早期版本。
