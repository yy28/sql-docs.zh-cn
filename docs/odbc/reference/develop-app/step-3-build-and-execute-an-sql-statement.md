---
title: 步骤3：生成并执行 SQL 语句 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114261"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>步骤 3：生成并执行 SQL 语句
第三步是生成和执行 SQL 语句，如下图所示。 用于执行此步骤的方法可能会有很大差异。 该应用程序可能会提示用户输入 SQL 语句，根据用户输入生成 SQL 语句，或者使用硬编码的 SQL 语句。 有关详细信息，请参阅[构造 SQL 语句](../../../odbc/reference/develop-app/constructing-sql-statements.md)。  
  
 ![显示如何生成和执行 SQL 语句](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 如果 SQL 语句包含参数，则应用程序通过为每个参数调用**SQLBindParameter** ，将这些参数绑定到应用程序变量中。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 生成 SQL 语句并绑定任何参数后，将通过**SQLExecDirect**执行语句。 如果语句将多次执行，则可以通过**SQLPrepare**准备，并通过**SQLExecute**执行。 有关详细信息，请参阅[执行语句](../../../odbc/reference/develop-app/executing-a-statement.md)。  
  
 应用程序还可以放弃地执行 SQL 语句，而调用函数返回包含目录信息的结果集，如可用的列或表。 有关详细信息，请参阅[目录数据的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 应用程序的下一操作取决于所执行的 SQL 语句的类型。  
  
|SQL 语句的类型|转到|  
|---------------------------|----------------|  
|**SELECT**或 catalog 函数|[步骤 4a：提取结果](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**UPDATE**、 **DELETE**或**INSERT**|[步骤 4b：提取行计数](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|所有其他 SQL 语句|步骤3：生成和执行 SQL 语句（本主题）或[步骤5：提交事务](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
