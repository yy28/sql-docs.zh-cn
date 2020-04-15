---
title: 应用 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9184986883f64bd082ca1db472d887609d3071bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306548"
---
# <a name="applications"></a>应用程序
*应用程序*是调用 ODBC API 访问数据的程序。 尽管许多类型的应用程序是可能的，但大多数分为三类，这些类别在整个本指南中用作示例。  
  
-   **通用应用程序**这些也称为收缩包装应用程序或现成的应用程序。 通用应用程序设计用于各种不同的 DBMS。 示例包括使用 ODBC 导入数据进行进一步分析的电子表格或统计信息包，以及使用 ODBC 从数据库获取邮件列表的字处理器。  
  
     通用应用程序的一个重要子类别是应用程序开发环境，如 PowerBuilder 或 Microsoft®可视化基本®。 尽管使用这些环境构建的应用程序可能只与单个 DBMS 一起工作，但环境本身需要使用多个 DBMS。  
  
     所有通用应用程序都有一个共同点，它们在 DBMS 之间高度互操作，并且需要以相对通用的方式使用 ODBC。 有关互操作性的详细信息，请参阅[选择互操作性级别](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直应用**垂直应用程序执行单一类型的任务，如订单输入或跟踪制造数据，并处理由应用程序开发人员控制的数据库架构。 对于特定客户，应用程序与单个 DBMS 一起工作。 例如，小型企业可能会将应用程序与 dBase 一起使用，而大型企业可能会将其与 Oracle 一起使用。  
  
     应用程序使用 ODBC 的方式使应用程序不绑定到任何一个 DBMS，尽管它可能与提供类似功能的有限数量的 DBMS 相关联。 因此，应用程序开发人员可以独立于 DBMS 销售应用程序。 垂直应用程序在开发时可互操作，但有时在客户选择 DBMS 后对其进行修改以包括不可互操作的代码。  
  
-   **自定义应用程序**自定义应用程序用于在单个公司中执行特定任务。 例如，大公司中的应用程序可能会从多个部门（每个部门使用不同的 DBMS）收集销售数据，并创建单个报表。 使用 ODBC 是因为它是一个通用接口，使程序员不必学习多个接口。 此类应用程序通常不可互操作，并写入特定的 DBMS 和驱动程序。  
  
 许多任务是所有应用程序共有的，无论它们如何使用 ODBC。 综合起来，它们在很大程度上定义了任何 ODBC 应用程序的流。 任务包括：  
  
-   选择数据源并连接到数据源。  
  
-   提交 SQL 语句以执行。  
  
-   检索结果（如果有）。  
  
-   处理错误。  
  
-   提交或回滚包围 SQL 语句的事务。  
  
-   与数据源断开连接。  
  
 由于大多数数据访问工作都使用 SQL 完成，因此应用程序使用 ODBC 的主要任务是提交 SQL 语句并检索这些语句生成的结果（如果有）。 应用程序使用 ODBC 的其他任务包括确定和调整驱动程序功能以及浏览数据库目录。
