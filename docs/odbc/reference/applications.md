---
title: "应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07ea2d2f08fb0d31ed141281b195742462350a5b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="applications"></a>应用程序
*应用程序*是一个程序，调用 ODBC API 访问数据。 虽然许多类型的应用程序可能，但大多数分为三个类别，用作本指南中的示例。  
  
-   **通用应用程序**这些也称为拆封授权应用程序或现成的应用程序。 通用应用程序用于处理各种不同 Dbms。 示例包括一个电子表格或统计信息包使用 ODBC 来导入数据以供进一步分析和使用 ODBC 来从数据库获取邮件列表字处理器。  
  
     通用应用程序的重要子类别是应用程序开发环境，如 PowerBuilder 或 Microsoft® Visual Basic®。 尽管可能会只使用单个 DBMS，构造使用这些环境的应用程序本身的环境需要使用多个 Dbms。  
  
     所有通用应用程序具有的共同点是，它们是在 Dbms 之间高度可互操作，它们需要使用 ODBC 相对通用的方式。 关于互操作性的详细信息，请参阅[选择的互操作级别性](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直应用程序**垂直应用程序执行单一类型的任务，例如订单条目或跟踪生产数据及使用应用程序的开发人员控制的数据库架构。 对于特定的客户，应用程序适用于单个 DBMS。 例如，小型企业可能会使用应用程序与 dBase，而的大型企业可能会使用它与 Oracle。  
  
     应用程序使用 ODBC 以此方式应用程序不会绑定到任何一个 DBMS，尽管它可能与有限数量的 Dbms 提供类似的功能。 因此，应用程序开发人员可以出售独立于 DBMS 应用程序。 当它们开发，但有时修改后的客户已选 DBMS 包括 noninteroperable 代码时，垂直应用程序进行互操作。  
  
-   **自定义应用程序**使用自定义应用程序以便在单个公司执行特定任务。 例如，大型公司中的应用程序可能从多个部门 （其中每个使用不同 DBMS） 收集销售数据，并创建单个报表。 使用 ODBC 是因为它是一个公共接口并使程序员不必了解多个接口。 此类应用程序通常是不可互操作和写入到特定 Dbms 和驱动程序。  
  
 大量的任务是通用的所有应用程序，无论他们如何使用 ODBC。 综上所述，他们很大程度上会定义任何 ODBC 应用程序流。 任务包括：  
  
-   选择数据源并连接到它。  
  
-   正在提交执行 SQL 语句。  
  
-   检索结果 （如果有）。  
  
-   处理错误。  
  
-   提交或回滚事务封闭的 SQL 语句。  
  
-   正在从数据源断开连接。  
  
 因为大多数数据访问工作使用 SQL 来完成，为其应用程序使用 ODBC 的主要任务是提交 SQL 语句和检索这些语句所生成的结果 （如果有）。 为其应用程序使用 ODBC 的其他任务包括确定和调整到驱动程序功能和浏览数据库目录。
