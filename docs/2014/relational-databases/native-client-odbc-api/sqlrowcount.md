---
title: SQLRowCount |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ae4c2fa55f5975357d94eaecb2f92e9468fee98f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125604"
---
# <a name="sqlrowcount"></a>SQLRowCount
  当参数值的数组绑定语句执行时`SQLRowCount`返回 SQL_ERROR，如果任何行的参数值在语句执行过程中生成的错误条件。 通过返回任何值*RowCountPtr*函数自变量。  
  
 应用程序可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性捕获在错误发生之前已处理的参数个数。  
  
 此外，应用程序还可以使用由状态值构成的数组（通过使用 SQL_ATTR_PARAM_STATUS_PTR 语句属性进行绑定），来捕获生成错误的参数行的数组偏移量。 应用程序可以遍历状态数组以确定已处理的实际行数。  
  
 当[!INCLUDE[tsql](../../includes/tsql-md.md)]执行插入、 更新、 DELETE 或 MERGE 语句包含 OUTPUT 子句，SQLRowCount 不会返回受影响之前已耗用结果集生成的 OUTPUT 子句中的所有行的行的计数。 到 sconsume 这些行，你调用 SQLFetch 或 SQLFetchScroll。 SQLResultCols 将返回-1，直到已耗用所有结果行。 SQLFetch 或 SQLFetchScroll 返回 SQL_NO_DATA 后，应用程序必须调用 SQLRowCount 若要确定在调用 SQLMoreResults 将移到下一个结果之前受影响的行数。  
  
## <a name="see-also"></a>请参阅  
 [SQLRowCount 函数](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  