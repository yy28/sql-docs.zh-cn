---
description: ODBC 解决方案
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f1a1c216dc67c33eadc9a058263087978f176297
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428859"
---
# <a name="the-odbc-solution"></a>ODBC 解决方案
问题在于，ODBC 是如何标准化数据库访问的呢？ 有两个体系结构要求：  
  
-   应用程序必须能够在不重新编译或重新链接的情况下，使用同一源代码访问多个 Dbms。  
  
-   应用程序必须能够同时访问多个 Dbms。  
  
 由于 marketplace 现实，还有一个问题：  
  
-   ODBC 应公开哪些 DBMS 功能？ 仅适用于所有 dbms 或任何 DBMS 中可用的任何功能的通用功能？  
  
 ODBC 通过以下方式解决这些问题：  
  
-   **ODBC 是一个调用级接口。** 为了解决应用程序使用相同的源代码访问多个 Dbms 的问题，ODBC 定义了标准 CLI。 这包含打开组和 ISO/IEC 中 CLI 规范的所有函数，并提供应用程序通常需要的其他功能。  
  
     支持 ODBC 的每个 DBMS 都需要不同的库（或驱动程序）。 驱动程序在 ODBC API 中实现函数。 若要使用其他驱动程序，则无需重新编译或重新链接应用程序。 相反，应用程序只是加载新的驱动程序，然后调用其中的函数。 若要同时访问多个 Dbms，应用程序将加载多个驱动程序。 如何支持驱动程序是特定于操作系统的。 例如，在 Microsoft® Windows®操作系统上，驱动程序是 (Dll) 的动态链接库。  
  
-   **ODBC 定义标准的 SQL 语法。** 除了标准调用级别接口外，ODBC 还定义标准的 SQL 语法。 此语法基于开放组 SQL CAE 规范。 这两种语法之间的差异很小，主要是因为嵌入式 SQL (打开) 组所需的 SQL 语法和 CLI (ODBC) 之间的差异。 此外，还提供了对语法的一些扩展，以公开开放组语法未涵盖的常用语言功能。  
  
     应用程序可以使用 ODBC 或 DBMS 特定的语法来提交语句。 如果语句使用的 ODBC 语法不同于 DBMS 特定的语法，则驱动程序会在将其发送到数据源之前对其进行转换。 但是，这种转换很少见，因为大多数 Dbms 已经使用了标准的 SQL 语法。  
  
-   **ODBC 提供了一个驱动程序管理器来管理多个 Dbms 的同时访问。** 尽管使用驱动程序可以解决同时访问多个 Dbms 的问题，但执行此操作的代码可能会很复杂。 设计为与所有驱动程序一起使用的应用程序不能静态链接到任何驱动程序。 相反，它们必须在运行时加载驱动程序，并通过函数指针的表调用这些驱动程序中的函数。 如果应用程序同时使用多个驱动程序，则情况会变得更加复杂。  
  
     ODBC 提供驱动程序管理器，而不是强制每个应用程序执行此操作。 驱动程序管理器实现所有 ODBC 函数（主要是在驱动程序中传递对 ODBC 函数的传递调用），并以静态方式链接到应用程序或在运行时由应用程序加载。 这样，应用程序就会按名称在驱动程序管理器中调用 ODBC 函数，而不是按每个驱动程序中的指针。  
  
     当应用程序需要特定的驱动程序时，它首先请求用于标识该驱动程序的连接句柄，然后请求驱动程序管理器加载该驱动程序。 驱动程序管理器加载驱动程序，并将每个函数的地址存储在驱动程序中。 若要调用驱动程序中的 ODBC 函数，应用程序会在驱动程序管理器中调用该函数，并传递驱动程序的连接句柄。 然后，驱动程序管理器使用之前存储的地址调用该函数。  
  
-   **ODBC 公开了大量 DBMS 功能，但并不要求驱动程序支持所有这些功能。** 如果 ODBC 只公开了对所有 Dbms 均通用的功能，则很少使用;毕竟，今天存在许多不同 Dbms 的原因是它们的功能不同。 如果 ODBC 公开了任何 DBMS 中提供的每项功能，驱动程序将无法实现。  
  
     相反，ODBC 公开了大量功能-超过大多数 Dbms 支持的功能-但需要驱动程序才能仅实现这些功能的子集。 仅当基础 DBMS 支持剩余功能时，驱动程序才会实现这些功能，或者，驱动程序会选择模拟它们。 因此，可以编写应用程序来利用单个 DBMS 的功能（如该 DBMS 的驱动程序所公开的功能），只使用所有 Dbms 所使用的功能，或检查特定功能是否受支持，并做出相应的响应。  
  
     为了使应用程序能够确定驱动程序和 DBMS 支持的功能，ODBC 提供了两个函数 (**SQLGetInfo** 和 **SQLGetFunctions**) ，可返回有关驱动程序和 dbms 功能的一般信息以及驱动程序支持的函数列表。 ODBC 还定义 API 和 SQL 语法一致性级别，这些级别指定了驱动程序支持的各种功能。 有关详细信息，请参阅 [一致性级别](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     请务必记住，ODBC 为它公开的所有功能定义了一个公共接口。 因此，应用程序包含特定于功能的代码，而不包含 DBMS 特定的代码，并可使用任何公开这些功能的驱动程序。 这样做的一个优点是，当 DBMS 支持的功能得到增强时，应用程序不需要进行更新;相反，当安装了更新的驱动程序时，应用程序会自动使用这些功能，因为其代码是特定于功能的，而不是特定于驱动程序或 DBMS 特定的。
