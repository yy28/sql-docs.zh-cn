---
title: 应用程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc655740701822d8c6ff9595327b906ee9a67026
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62734993"
---
# <a name="applications"></a>应用程序
*应用程序*是调用 ODBC API 访问数据的程序。 尽管许多类型的应用程序可能，但大多数划分为三个类别，用作在本指南中的示例。  
  
-   **通用应用程序**这些也称为打包应用程序或现成的应用程序。 通用应用程序用于处理各种不同的 Dbms。 示例包括电子表格或使用 ODBC 来导入数据以供进一步分析的统计信息包，并使用 ODBC 来从数据库获取邮件列表的字处理器。  
  
     重要的子类别的通用应用程序是应用程序开发环境，如 PowerBuilder 或 Microsoft® Visual Basic®。 尽管使用这些环境构建的应用程序可能只使用单个 DBMS，环境本身需要能够处理多个 Dbms。  
  
     所有通用应用程序具有的共同点是，它们是在 Dbms 之间高度可互操作，它们需要使用 ODBC 相对较通用的方式。 有关互操作性的详细信息，请参阅[选择的互操作级别性](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直应用程序**垂直应用程序执行单一类型的任务，例如订单录入或跟踪生产数据和使用由应用程序的开发人员控制的数据库架构。 对于特定的客户，应用程序处理单个 DBMS。 例如，小型企业可能会使用该应用程序 dBase，而大型企业可能使用它与 Oracle。  
  
     尽管它可能会绑定到有限数量的 Dbms 提供类似的功能，应用程序中应用程序未绑定到任何一个 DBMS，这种方式使用 ODBC。 因此，应用程序开发人员可以销售应用程序独立于 DBMS。 开发但有时会被修改为客户选择 DBMS 后包括 noninteroperable 代码时，垂直应用程序进行互操作。  
  
-   **自定义应用程序**自定义应用程序都用于在一家公司中执行特定任务。 例如，一家大型公司中的应用程序可能从多个部门 （其中每个使用不同的 DBMS） 中收集销售数据，并创建单个报表。 使用 ODBC，因为它是一个通用接口，使程序员无需了解多个接口。 此类应用程序中通常无法进行互操作性，并写入到特定 Dbms 和驱动程序。  
  
 多个任务是通用的所有应用程序，无论他们如何使用 ODBC。 它们合起来看，很大程度上定义任何 ODBC 应用程序的流。 任务包括：  
  
-   选择数据源并连接到它。  
  
-   正在提交用于执行 SQL 语句。  
  
-   正在检索结果 （如果有）。  
  
-   处理错误。  
  
-   提交或回滚封闭的 SQL 语句的事务。  
  
-   断开与数据源的连接。  
  
 由于大多数数据访问工作通过 SQL，对其应用程序使用 ODBC 的主要任务是提交 SQL 语句并检索这些语句生成的结果 （如果有）。 为其应用程序使用 ODBC 的其他任务包括确定并对驱动程序功能的调整和浏览数据库目录。
