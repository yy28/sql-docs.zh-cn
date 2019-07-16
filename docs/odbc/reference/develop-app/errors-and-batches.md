---
title: 错误和批处理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6902b82c74e953d6009d7e5352608477d92122d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051128"
---
# <a name="errors-and-batches"></a>错误和批处理
执行一批 SQL 语句时出现错误时，以下四个结果中的一个可能会出现。 （每个可能结果是数据源特定于和甚至可能取决于包括在批中的语句。）  
  
-   不执行批处理中的任何语句。  
  
-   批处理中的任何语句执行和回滚事务。  
  
-   执行所有的错误语句前的语句。  
  
-   执行所有除错误语句的语句。  
  
 在前两个情况下， **SQLExecute**并**SQLExecDirect**返回 SQL_ERROR。 在后一种两种情况下，它们可能会返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，具体取决于实现。 在所有情况下，进一步错误的信息可通过检索**SQLGetDiagField**， **SQLGetDiagRec**，或**SQLError**。 但是，此信息的深度和性质是数据源特定于。 此外，此信息不太准确地识别错误中的语句。
