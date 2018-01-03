---
title: "步骤 3： 生成并执行的 SQL 语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc0aebc832ff451ab302636c7621b008bec4da1d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步骤 3： 生成并执行的 SQL 语句
第三步是生成和执行 SQL 语句，如下面的插图中所示。 用于执行此步骤的方法很可能有很大差异。 应用程序可能会提示用户输入的 SQL 语句，生成基于用户输入的 SQL 语句或使用硬编码的 SQL 语句。 有关详细信息，请参阅[构造 SQL 语句](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![显示生成和执行 SQL 语句](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 语句中包含参数，应用程序将它们绑定到应用程序变量通过调用**SQLBindParameter**每个参数。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 生成 SQL 语句和任何参数绑定后，执行该语句时使用**SQLExecDirect**。 如果将多次执行语句，它可准备与**SQLPrepare**和执行与**SQLExecute**。 有关详细信息，请参阅[执行语句](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 应用程序可能还放弃完全执行 SQL 语句，并改为调用函数返回一个包含目录信息，如可用列或表的结果集。 有关详细信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 应用程序的下一步操作取决于执行 SQL 语句的类型。  
  
|SQL 语句的类型|继续执行|  
|---------------------------|----------------|  
|**选择**或目录函数|[步骤 4a：提取结果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**，**删除**，或**插入**|[步骤 4b：提取行计数](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 语句|步骤 3： 生成并执行的 SQL 语句 （本主题） 或[步骤 5： 提交事务](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
