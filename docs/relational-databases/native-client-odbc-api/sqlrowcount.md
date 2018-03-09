---
title: SQLRowCount | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ade5cc43655bf92b9f7b3355f666efee0715200a
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  当参数值的数组绑定语句执行时**SQLRowCount**返回 SQL_ERROR，如果任何行的参数值在语句执行过程中生成的错误条件。 通过返回任何值*RowCountPtr*函数自变量。  
  
 应用程序可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性捕获在错误发生之前已处理的参数个数。  
  
 此外，应用程序还可以使用由状态值构成的数组（通过使用 SQL_ATTR_PARAM_STATUS_PTR 语句属性进行绑定），来捕获生成错误的参数行的数组偏移量。 应用程序可以遍历状态数组以确定已处理的实际行数。  
  
 当[!INCLUDE[tsql](../../includes/tsql-md.md)]执行插入、 更新、 DELETE 或 MERGE 语句包含 OUTPUT 子句，SQLRowCount 不会返回受影响之前已耗用结果集生成的 OUTPUT 子句中的所有行的行的计数。 到 sconsume 这些行，你调用 SQLFetch 或 SQLFetchScroll。 SQLResultCols 将返回-1，直到已耗用所有结果行。 SQLFetch 或 SQLFetchScroll 返回 SQL_NO_DATA 后，应用程序必须调用 SQLRowCount 若要确定在调用 SQLMoreResults 将移到下一个结果之前受影响的行数。  
  
## <a name="see-also"></a>另请参阅  
 [SQLRowCount 函数](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
