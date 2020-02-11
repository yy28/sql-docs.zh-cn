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
ms.openlocfilehash: f15b5e8eb6eb7c63ab771030f0c31e8c9ff92724
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135678"
---
# <a name="applications"></a>应用程序
*应用程序*是调用 ODBC API 来访问数据的程序。 尽管许多类型的应用程序都是可行的，但大多数情况下都是三个类别，在本指南中作为示例使用。  
  
-   **通用应用程序**这些应用程序也称为收缩包装应用程序或现成的应用程序。 一般的应用程序设计为适用于各种不同 Dbms。 例如，使用 ODBC 导入数据以进行进一步分析的电子表格或统计信息包以及使用 ODBC 从数据库获取邮件列表的字处理器。  
  
     一般应用程序的一个重要子类别是应用程序开发环境，如 PowerBuilder 或 Microsoft® Visual Basic®。 尽管使用这些环境构建的应用程序可能仅适用于单个 DBMS，环境本身也需要使用多个 Dbms。  
  
     所有通用应用程序的共同之处在于它们在 Dbms 之间高度可互操作，并且需要以相对通用的方式使用 ODBC。 有关互操作性的详细信息，请参阅[选择级别的互操作性](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)。  
  
-   **垂直应用程序**垂直应用程序执行一种类型的任务，例如订单输入或跟踪制造数据，并使用由应用程序开发人员控制的数据库架构。 对于特定客户，应用程序可以使用单个 DBMS。 例如，小型企业可能会将该应用程序与 dBase 一起使用，而大型企业可能会将其与 Oracle 一起使用。  
  
     应用程序以这种方式使用 ODBC，因为它可能与提供类似功能的有限数量的 Dbms 相关联。 这样，应用程序开发人员便可以独立于 DBMS 销售应用程序了。 当客户选择 DBMS 后，垂直应用程序可以互操作，但有时将其修改为包含 noninteroperable 的代码。  
  
-   **自定义应用程序**自定义应用程序用于在单个公司中执行特定任务。 例如，大型公司中的应用程序可能会从多个部门收集销售数据（每个部门使用不同的 DBMS），并创建一个报表。 使用 ODBC 是因为它是一个公共接口，并使程序员不必了解多个接口。 此类应用程序通常不可互操作，并且已写入特定 Dbms 和驱动程序。  
  
 许多任务对于所有应用程序都是通用的，不管它们使用 ODBC 的方式如何。 它们共同定义了任何 ODBC 应用程序的流。 任务包括：  
  
-   选择数据源并连接到该数据源。  
  
-   提交要执行的 SQL 语句。  
  
-   检索结果（如果有）。  
  
-   处理错误。  
  
-   提交或回滚包含 SQL 语句的事务。  
  
-   正在从数据源断开连接。  
  
 由于大多数数据访问都是通过 SQL 来完成的，因此，应用程序使用 ODBC 的主要任务是提交 SQL 语句并检索这些语句生成的结果（如果有）。 应用程序使用 ODBC 的其他任务包括确定和调整驱动程序功能以及浏览数据库目录。
