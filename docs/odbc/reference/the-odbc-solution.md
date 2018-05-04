---
title: ODBC 解决方案 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f028b4e452f1318f7f0142f7b41e06fc8ced368
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="the-odbc-solution"></a>ODBC 解决方案
问题，然后，是 ODBC 如何标准化数据库访问权限？ 有两个体系结构要求：  
  
-   应用程序必须能够访问而无需重新编译或重新链接使用相同的源代码的多个 Dbms。  
  
-   应用程序必须能够同时访问多个 Dbms。  
  
 还有一个更多问题，由于 marketplace 现实：  
  
-   ODBC 应公开的 DBMS 功能？ 仅公用的所有 Dbms 或任何功能，则在任何 DBMS 中可用的功能？  
  
 ODBC 按以下方式解决了这些问题：  
  
-   **ODBC 是调用级接口。** 若要解决此问题的应用程序如何访问多个使用相同的源代码的 Dbms，ODBC 定义标准 CLI。 该文件包含所有从 Open Group 和 ISO/IEC 的 CLI 规范中的函数并提供通常由应用程序所需的其他函数。  
  
     不同的库或驱动程序，需要为每个支持 ODBC 的 DBMS。 该驱动程序实现中 ODBC API 函数。 若要使用不同的驱动程序，应用程序不必重新编译或重新链接。 相反，应用程序只需加载新的驱动程序，并在其中调用函数。 若要同时访问多个 Dbms，应用程序加载多个驱动程序。 如何支持驱动程序是特定于操作系统 –。 例如，在 Microsoft® Windows® 操作系统、 驱动程序都是动态链接库 (Dll)。  
  
-   **ODBC 定义标准的 SQL 语法。** 除了标准的调用级界面，ODBC 定义标准的 SQL 语法。 此语法取决于打开组 SQL CAE 规范。 两种语法之间的差异十分微小和主要是由于所需的 SQL 语法之间的差异嵌入 SQL (Open Group) 和 CLI (ODBC)。 也有一些扩展可公开未涵盖的 Open Group 语法通常可用的语言功能的语法。  
  
     应用程序可以提交使用 ODBC 或特定于 DBMS 的语法的语句。 如果语句使用 ODBC 语法不同于特定于 DBMS 的语法，驱动程序会将其转换发送到数据源之前。 但是，此类转换很少出现，因为大多数 Dbms 已使用标准 SQL 语法。  
  
-   **ODBC 提供的驱动程序管理器来管理对多个 Dbms 的同时进行访问。** 尽管使用驱动程序解决了同时访问多个 Dbms 的问题，要执行此操作的代码可能很复杂。 用于处理所有驱动程序的应用程序无法以静态方式链接到任何驱动程序。 相反，它们必须在运行时加载驱动程序，通过函数指针的表中调用的函数。 这种情况变得更加复杂，如果应用程序同时使用多个驱动程序。  
  
     而不强制执行此操作每个应用程序，ODBC 提供了驱动程序管理器。 驱动程序管理器实现所有 ODBC 函数-多半以传递到 ODBC 驱动程序中的函数的调用-和静态链接到应用程序或在运行时应用程序加载的。 因此，在应用程序调用 ODBC 函数，按名称在驱动程序管理器中，而不是在每个驱动程序的指针。  
  
     当应用程序需要特定的驱动程序时，它首先请求用来确定驱动程序和驱动程序管理器加载的驱动程序的请求的连接句柄。 驱动程序管理器将加载驱动程序，并将每个函数的地址存储驱动程序中。 若要驱动程序中调用 ODBC 函数，该应用程序调用该函数在驱动程序管理器中，并将连接句柄传递驱动程序。 驱动程序管理器然后通过使用以前存储的地址调用该函数。  
  
-   **ODBC 公开大量 DBMS 功能，但不需要驱动程序以支持所有这些。** 如果 ODBC 公开共有所有 Dbms 的功能，它的作用很少用到;毕竟，原因以便目前存在许多不同 Dbms 是它们具有不同的功能。 如果 ODBC 公开每个可用于任何 DBMS 的功能，它就不可能实现驱动程序。  
  
     相反，ODBC 公开大量功能-超过支持的大多数 Dbms-，但需要驱动程序以实现这些功能的一个子集。 驱动程序实现其余功能，仅当它们支持的基础的 DBMS 或如果他们选择模拟它们。 因此，应用程序可以编写为利用单个 DBMS 的功能公开的驱动程序该 DBMS，要使用的所有 Dbms，使用这些功能，或者要检查的特定功能的支持并相应地作出反应。  
  
     ODBC，以便应用程序可以确定哪些功能驱动程序和 DBMS 支持，提供两个函数 (**SQLGetInfo**和**SQLGetFunctions**) 返回的驱动程序和 DBMS 的常规信息功能和函数的列表的驱动程序支持。 ODBC 还定义了 API 和 SQL 语法一致性级别，这些级别指定的驱动程序支持的功能的广泛范围。 有关详细信息，请参阅[一致性级别](../../odbc/reference/develop-app/conformance-levels.md)。  
  
     请务必记住 ODBC 定义的所有功能，它公开的公共接口。 因此，应用程序包含特定于功能的代码，不是特定于 DBMS 的代码，并且可以使用的任何驱动程序公开那些功能。 这一个优点是，应用程序不需要在 DBMS 支持的功能已得到增强，; 时更新相反，当安装更新的驱动程序时，应用程序自动使用功能因为其代码是特定于功能的、 不是特定于驱动程序或特定于 DBMS 的。
