---
title: 步骤 3：生成并执行 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0e369b74ef629c5fd7136b9098f579b5ad2b1b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114261"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步骤 3：生成并执行 SQL 语句
第三步是生成和执行 SQL 语句，如以下插图所示。 用于执行此步骤的方法很可能有很大差异。 应用程序可能会提示用户输入的 SQL 语句，生成基于用户输入的 SQL 语句或使用硬编码的 SQL 语句。 有关详细信息，请参阅[构造 SQL 语句](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![显示了生成和执行 SQL 语句](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 语句中包含参数，该应用程序将它们绑定到应用程序变量通过调用**SQLBindParameter**为每个参数。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 生成 SQL 语句并将其绑定所有参数后，执行语句**SQLExecDirect**。 如果将多次执行语句，它可以请准备好**SQLPrepare**并执行与**SQLExecute**。 有关详细信息，请参阅[执行语句](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 应用程序可能还会放弃完全执行 SQL 语句，并改为调用一个函数来返回结果集包含目录信息，例如可用列或表。 有关详细信息，请参阅[使用的目录数据](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 应用程序的下一步操作取决于执行 SQL 语句的类型。  
  
|SQL 语句的类型|请继续执行|  
|---------------------------|----------------|  
|**选择**或目录函数|[步骤 4a:提取的结果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**更新**，**删除**，或**插入**|[步骤 4b:提取行计数](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 语句|步骤 3：生成并执行 SQL 语句 （本主题中） 或[步骤 5:提交事务](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
