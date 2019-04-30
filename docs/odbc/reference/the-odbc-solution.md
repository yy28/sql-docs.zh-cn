---
title: ODBC 解决方案 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5adf32800f4c2bc2b4a0874ca7efc22f04ffd110
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200472"
---
# <a name="the-odbc-solution"></a>ODBC 解决方案
然后，问题是 ODBC 如何标准化数据库访问权限？ 有两个体系结构要求：  
  
-   应用程序必须能够访问而无需重新编译或重新链接使用相同的源代码的多个 Dbms。  
  
-   应用程序必须能够同时访问多个 Dbms。  
  
 还有一个更多问题，由于 marketplace 现实：  
  
-   ODBC 应公开的 DBMS 功能？ 只是普遍适用于所有 Dbms 或任何功能，则可在任何 DBMS 的功能？  
  
 ODBC 按以下方式解决这些问题：  
  
-   **ODBC 是一个调用级别接口。** 若要解决此问题的应用程序访问多个 Dbms 使用相同的源代码的方式，ODBC 定义标准的 CLI。 该文件包含所有从 Open Group 和 ISO/IEC CLI 规范中的函数并提供的应用程序通常所需的附加功能。  
  
     不同的库或驱动程序，需要为每个支持 ODBC 的 DBMS。 该驱动程序实现中 ODBC API 函数。 若要使用不同的驱动程序，该应用程序不必重新编译或重新链接。 相反，应用程序只需加载新的驱动程序，并在它调用的函数。 若要同时访问多个 Dbms，应用程序加载多个驱动程序。 如何支持驱动程序是特定于操作系统的。 例如，在 Microsoft® Windows® 操作系统、 驱动程序都是动态链接库 (Dll)。  
  
-   **ODBC 定义标准的 SQL 语法。** 除了标准调用级别接口，ODBC 定义了标准的 SQL 语法。 此语法取决于打开组 SQL CAE 规范。 两种语法之间的差异是次要和主要是由于所需的 SQL 语法之间的差异嵌入的 SQL (Open Group) 和 CLI (ODBC)。 也有一些扩展到公开通常可用的语言功能不受 Open Group 语法的语法。  
  
     应用程序可以提交语句使用 ODBC 或特定于 DBMS 的语法。 如果一个语句使用 ODBC 语法不同于特定于 DBMS 的语法，该驱动程序会将其转换之前将其发送到数据源。 但是，这种转换很少，因为大多数 Dbms 已使用标准 SQL 语法。  
  
-   **ODBC 提供了驱动程序管理器来管理对多个 Dbms 的同时进行访问。** 尽管使用驱动程序可以解决问题的同时访问多个 Dbms，若要执行此操作的代码可能很复杂。 用于处理的所有驱动程序的应用程序无法以静态方式链接到的任何驱动程序。 相反，它们必须在运行时加载驱动程序，并在其中通过函数指针的表调用的函数。 这种情况变得更加复杂，如果应用程序同时使用多个驱动程序。  
  
     而不是强制执行此操作每个应用程序时，ODBC 提供了驱动程序管理器。 驱动程序管理器实现的所有 ODBC 函数的主要作为传递到驱动程序-中的 ODBC 函数调用和以静态方式链接到应用程序或应用程序在运行时加载。 因此，应用程序调用 ODBC 函数名称在驱动程序管理器中，而不是由每个驱动程序中的指针。  
  
     当应用程序需要特定的驱动程序时，它首先请求连接句柄，用来确定驱动程序和驱动程序管理器加载的驱动程序的请求。 驱动程序管理器加载驱动程序，并将每个函数的地址存储在驱动程序。 若要在驱动程序中调用 ODBC 函数，该应用程序将调用该函数在驱动程序管理器，并将连接句柄传递的驱动程序。 然后，驱动程序管理器通过使用以前存储的地址调用的函数。  
  
-   **ODBC 公开大量的 DBMS 功能，但不需要驱动程序以支持所有这些。** 如果 ODBC 公开是普遍适用于所有 Dbms 的功能，那就是几乎没有什么用处;毕竟，原因目前存在许多不同 Dbms 是它们具有不同的功能。 如果 ODBC 公开的每个功能是可在任何 DBMS，它就不可能实现的驱动程序。  
  
     相反，ODBC 公开大量的功能的多个支持的大多数 Dbms 的但需要驱动程序，以实现这些功能的一个子集。 仅当它们由基础 DBMS 支持或如果用户选择模拟它们，驱动程序实现其余功能。 因此，可以编写应用程序来公开该 DBMS，要使用所有 Dbms 都使用的这些功能，或者要检查的特定功能的支持，并采取相应的驱动程序通过利用单个 DBMS 的功能。  
  
     因此，应用程序可以确定哪些功能驱动程序和 DBMS 支持，ODBC 提供了两个函数 (**SQLGetInfo**并**SQLGetFunctions**) 返回的驱动程序和 DBMS 的常规信息功能和函数的列表的驱动程序支持。 ODBC 还定义了 API 和 SQL 语法的一致性级别，这些级别指定的驱动程序支持的功能的广泛范围。 有关详细信息，请参阅[一致性级别](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     请务必记住 ODBC 定义的所有功能，它公开一个公共接口。 因此，应用程序包含特定于功能的代码，不是特定于 DBMS 的代码，并且可以使用任何公开这些功能的驱动程序。 其中一个优点是，应用程序不需要 DBMS 支持的功能已得到增强，; 时进行更新相反，安装更新的驱动程序时，应用程序自动使用功能因为其代码是特定于功能的、 不特定于驱动程序或特定于 DBMS 的。
