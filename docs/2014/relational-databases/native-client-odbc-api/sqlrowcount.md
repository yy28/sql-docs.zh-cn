---
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff2a744f68cf6152330179eb8dcab1f33911914
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046602"
---
# <a name="sqlrowcount"></a>SQLRowCount
  当参数值的数组绑定的语句执行时`SQLRowCount`如果任何行的参数值在语句执行过程中生成错误条件，则返回 SQL_ERROR。 通过返回任何值*RowCountPtr*函数自变量。  
  
 应用程序可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性捕获在错误发生之前已处理的参数个数。  
  
 此外，应用程序还可以使用由状态值构成的数组（通过使用 SQL_ATTR_PARAM_STATUS_PTR 语句属性进行绑定），来捕获生成错误的参数行的数组偏移量。 应用程序可以遍历状态数组以确定已处理的实际行数。  
  
 当[!INCLUDE[tsql](../../includes/tsql-md.md)]执行带有 OUTPUT 子句的 INSERT、 UPDATE、 DELETE 或 MERGE 语句、 SQLRowCount 不会返回受影响之前已使用中的 OUTPUT 子句生成的结果集的所有行的行计数。 若这些行，请使用 SQLFetch 或 SQLFetchScroll。 SQLResultCols 将返回-1，直到所有结果行都为止。 SQLFetch 或 SQLFetchScroll 返回 sql_no_data 指示到达后，应用程序必须调用 SQLRowCount 来确定调用 SQLMoreResults 移动到下一个结果之前受影响的行数。  
  
## <a name="see-also"></a>请参阅  
 [SQLRowCount 函数](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
