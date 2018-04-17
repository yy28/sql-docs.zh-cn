---
title: 错误和批处理 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e742c6330ad4106217068bdc7a145b208af51d2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="errors-and-batches"></a>错误和批处理
如果在执行一批 SQL 语句时发生错误，以下四种结果之一是可能的。 （每个可能结果是数据源 – 特定，甚至可能取决于包含批处理中的语句。）  
  
-   不执行批处理中的任何语句。  
  
-   不执行批处理中的任何语句，事务将回滚。  
  
-   执行所有之前的错误语句的语句。  
  
-   执行所有除 error 语句的语句。  
  
 在前两个情况下， **SQLExecute**和**SQLExecDirect**返回 SQL_ERROR。 在后一种的两个情况下，它们可能返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，具体取决于实现。 在所有情况下，进一步错误信息可以检索与**SQLGetDiagField**， **SQLGetDiagRec**，或**SQLError**。 但是的性质和深度此信息是数据源 – 特定。 此外，此信息不太准确地识别错误中的语句。
