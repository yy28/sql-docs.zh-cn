---
title: 错误和批次 |微软文档
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
ms.openlocfilehash: 36a402686a695a08748df24a7b40a228d7a2ca7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300427"
---
# <a name="errors-and-batches"></a>错误和批处理
当执行一批 SQL 语句时发生错误时，可能会出现以下四个结果之一。 （每个可能的结果都是特定于数据源的，甚至可能取决于批处理中包含的语句。  
  
-   未执行批处理中的语句。  
  
-   未执行批处理中的语句，并且事务将回滚。  
  
-   执行错误语句之前的所有语句。  
  
-   除错误语句之外的所有语句都执行。  
  
 在前两种情况下 **，SQLExecute**和**SQLExecDirect**返回SQL_ERROR。 在后两种情况下，它们可能返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS，具体取决于实现。 在所有情况下，可以使用**SQLGetDiagField、SQLGetDiagRec**或**SQLGetDiagRec** **SQLError**检索进一步的错误信息。 但是，此信息的性质和深度是特定于数据源的。 此外，此信息不可能准确识别错误语句。
