---
title: "类型的应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26835fa277391f359d628ec25c03d38364e398e7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-applications"></a>类型的应用程序
ODBC 应用程序可以进行分类，如下所示：  
  
-   **纯 ODBC 2。**  
     ***x*应用程序**的 32 位应用程序的：  
  
    -   调用仅 ODBC 2。*x*函数 (包括 ODBC 1.0 函数**SQLSetParam**)。 其中包括 ODBC 1。*x*都已进行迁移到 32 位的应用程序。  
  
    -   需要 ODBC 2。*x*有行为更改的功能的行为。 (请参阅[行为更改](../../../odbc/reference/develop-app/behavioral-changes.md)有关详细信息。)  
  
    -   不重新编译使用 ODBC 3.5 标头。  
  
-   **纯 ODBC 2。**  
     ***x*重新编译应用程序**纯 ODBC 2。*x*已使用了 ODBC 3.5 标头文件，重新编译的应用程序通过设置 ODBCVER = 0x0250。  
  
-   **纯 ODBC 2。**  
     ***x* Unicode 应用程序**纯 ODBC 2。*x*重新编译应用程序是符合 Unicode 的并且使用 SQL_WCHAR 数据类型。  
  
-   **纯打开组和 ISO**–**符合 ODBC 应用程序**的 32 位应用程序的：  
  
    -   调用 Open Group 或 ISO CLI 标准中定义的函数。 （这些函数可能包括不推荐使用 3.0 函数。）  
  
    -   不使用 Unicode 数据类型。  
  
    -   需要有行为更改的功能的 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.0 应用程序**的 32 位应用程序的：  
  
    -   使用 3.0 标头编译。  
  
    -   调用任何 ODBC 3.0 函数时，可能包括那些已被否决。  
  
    -   需要有行为更改的功能的 ODBC 3.0 行为。  
  
-   **纯 ODBC 3.5 应用程序**32 或 64 位应用程序的：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.5 函数时，可能包括那些已被否决。  
  
    -   需要有行为更改的功能的 ODBC 3.5 行为。  
  
-   **纯 ODBC 3.8 （或更高版本） 应用程序**的 32 位或 64 位应用程序的：  
  
    -   可以使用 Unicode 数据类型。  
  
    -   调用任何 ODBC 3.8 函数时，可能包括那些已被否决。  
  
    -   需要有行为更改的功能的 ODBC 3.8 行为。  
  
-   **替换为应用程序**32 或 64 位应用程序的：  
  
    -   实现重复功能的新行为。  
  
    -   仅在条件代码内 ODBC 的更高版本中使用的任何新功能。  
  
    -   具有有限的条件的代码来处理行为的更改或已将自己为早期版本的 ODBC 应用程序注册。

