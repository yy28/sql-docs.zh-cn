---
description: 错误和批处理
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5cdf4d394ffa1c17173aedc4485b6979cf371e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461489"
---
# <a name="errors-and-batches"></a>错误和批处理
当执行一批 SQL 语句时出错时，可能会出现以下四种结果之一。  (每个可能的结果都是特定于数据源，甚至可能依赖于批处理中包含的语句。 )   
  
-   不执行批处理中的任何语句。  
  
-   不会执行批处理中的任何语句，并回滚事务。  
  
-   执行 error 语句之前的所有语句。  
  
-   执行除 error 语句以外的所有语句。  
  
 在前两种情况下， **SQLExecute** 和 **SQLExecDirect** 返回 SQL_ERROR。 在后两种情况下，它们可能会返回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，具体取决于实现。 在所有情况下，都可以通过 **SQLGetDiagField**、 **SQLGetDiagRec**或 **SQLError**检索更多错误信息。 但是，此信息的性质和深度是特定于数据源的。 此外，此信息不可能准确地识别出错的语句。
