---
title: SQLRowCount |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3cfb76dbd1732e32238c484f589d3b4696ff89d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302295"
---
# <a name="sqlrowcount"></a>SQLRowCount
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  当参数值数组绑定为语句执行时，如果任何参数值行在语句执行中生成错误条件 **，SQLRowCount**将返回SQL_ERROR。 不通过函数的*RowCountPtr*参数返回任何值。  
  
 应用程序可以利用 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性捕获在错误发生之前已处理的参数个数。  
  
 此外，应用程序还可以使用由状态值构成的数组（通过使用 SQL_ATTR_PARAM_STATUS_PTR 语句属性进行绑定），来捕获生成错误的参数行的数组偏移量。 应用程序可以遍历状态数组以确定已处理的实际行数。  
  
 执行具有[!INCLUDE[tsql](../../includes/tsql-md.md)]OUTPUT 子句的插入、更新、删除或 MERGE 语句时，SQLRowCount 不会返回受影响的行计数，直到使用 OUTPUT 子句生成的结果集中的所有行。 要消耗这些行，请致电 SQLFetch 或 SQLFetchScroll。 SQLResultCols 将返回 -1，直到使用所有结果行。 在 SQLFetch 或 SQLFetch 返回SQL_NO_DATA后，应用程序必须调用 SQLRowCount 以确定受影响的行数，然后再调用 SQLMoreResult 移动到下一个结果。  
  
## <a name="see-also"></a>另请参阅  
 [SQLRowCount 函数](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
