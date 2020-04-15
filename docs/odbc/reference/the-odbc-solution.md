---
title: ODBC 解决方案 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b35883ff4d621f0ecc092020ad744455281dd63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286750"
---
# <a name="the-odbc-solution"></a>ODBC 解决方案
那么，问题是ODBC如何标准化数据库访问？ 有两个体系结构要求：  
  
-   应用程序必须能够使用相同的源代码访问多个 DBMS，而无需重新编译或重新链接。  
  
-   应用程序必须能够同时访问多个 DBMS。  
  
 由于市场现实，还有一个问题：  
  
-   应公开哪些 DBMS 功能？ 只有所有 DBMS 共有的功能或任何 DBMS 中可用的功能？  
  
 ODBC 以以下方式解决了这些问题：  
  
-   **ODBC 是一个呼叫级接口。** 为了解决应用程序如何使用同一源代码访问多个 DBM 的问题，ODBC 定义了标准 CLI。 它包含开放组和 ISO/IEC CLI 规范中的所有功能，并提供应用程序通常要求的其他功能。  
  
     支持 ODBC 的每个 DBMS 都需要不同的库或驱动程序。 驱动程序在 ODBC API 中实现函数。 要使用其他驱动程序，不需要重新编译或重新链接应用程序。 相反，应用程序只需加载新驱动程序并调用其中的函数。 要同时访问多个 DBMS，应用程序将加载多个驱动程序。 支持驱动程序的方式特定于操作系统。 例如，在 Microsoft® Windows ®操作系统上，驱动程序是动态链接库 （DLL）。  
  
-   **ODBC 定义了标准的 SQL 语法。** 除了标准调用级接口外，ODBC 还定义了标准的 SQL 语法。 此语法基于开放组 SQL CAE 规范。 这两种语法之间的差异很小，这主要是因为嵌入式 SQL（开放组）和 CLI （ODBC） 所需的 SQL 语法之间的差异。 还有一些语法扩展，以公开开放组语法未涵盖的常用语言功能。  
  
     应用程序可以使用 ODBC 或 DBMS 特定的语法提交语句。 如果语句使用的 ODBC 语法不同于特定于 DBMS 的语法，则驱动程序在将其发送到数据源之前将其转换。 但是，此类转换很少见，因为大多数 DBMS 已经使用标准 SQL 语法。  
  
-   **ODBC 提供了一个驱动程序管理器来管理对多个 DBMS 的同步访问。** 尽管驱动程序的使用解决了同时访问多个 DBMS 的问题，但这样做的代码可能很复杂。 设计用于所有驱动程序的应用程序不能以静态方式链接到任何驱动程序。 相反，它们必须在运行时加载驱动程序，并通过函数指针表调用其中的函数。 如果应用程序同时使用多个驱动程序，情况将变得更加复杂。  
  
     ODBC 不是强制每个应用程序执行此操作，而是提供了一个驱动程序管理器。 驱动程序管理器实现所有 ODBC 函数（主要是在驱动程序中作为对 ODBC 函数的传递调用），并静态链接到应用程序或在运行时由应用程序加载。 因此，应用程序在驱动程序管理器中按名称调用 ODBC 函数，而不是按每个驱动程序中的指针调用。  
  
     当应用程序需要特定驱动程序时，它首先请求一个连接句柄来标识驱动程序，然后请求驱动程序管理器加载驱动程序。 驱动程序管理器加载驱动程序并将每个函数的地址存储在驱动程序中。 要在驱动程序中调用 ODBC 函数，应用程序将调用驱动程序管理器中的该函数并传递驱动程序的连接句柄。 然后，驱动程序管理器使用它之前存储的地址调用函数。  
  
-   **ODBC 公开了大量的 DBMS 功能，但不需要驱动程序来支持所有这些功能。** 如果 ODBC 只公开所有 DBMS 共有的功能，则使用很少;毕竟，今天存在这么多不同的DBMS的原因是它们有不同的功能。 如果 ODBC 公开了任何 DBMS 中可用的所有功能，则驱动程序将无法实现。  
  
     相反，ODBC 公开了大量的功能（比大多数 DBMS 支持的功能更多），但要求驱动程序仅实现这些功能的子集。 仅当基础 DBMS 支持这些功能或选择模拟这些功能时，驱动程序才实现这些功能。 因此，可以编写应用程序来利用该 DBMS 的驱动程序公开的单个 DBMS 的功能，仅使用所有 DBBMS 使用的功能，或者检查对特定功能的支持并做出相应反应。  
  
     以便应用程序可以确定驱动程序和 DBMS 支持的功能，ODBC 提供了两个函数 **（SQLGetInfo**和**SQLGet功能**），返回有关驱动程序和 DBMS 功能的一般信息以及驱动程序支持的函数列表。 ODBC 还定义了 API 和 SQL 语法一致性级别，这些级别指定驱动程序支持的广泛功能范围。 有关详细信息，请参阅[一致性级别](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     请务必记住，ODBC 为其公开的所有功能定义了通用接口。 因此，应用程序包含特定于功能的代码，而不是特定于 DBMS 的代码，并且可以使用公开这些功能的任何驱动程序。 这样做的一个优点是，当 DBMS 支持的功能得到增强时，不需要更新应用程序;相反，在安装更新的驱动程序时，应用程序会自动使用这些功能，因为它的代码特定于功能，而不是特定于驱动程序或特定于 DBMS。
