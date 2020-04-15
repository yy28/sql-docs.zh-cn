---
title: ODBC 光标库错误代码 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c263ce53c41546e63dc2a830d3db3b903e2e3515
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301428"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 游标库错误代码
> [!IMPORTANT]  
>  此功能将在 Microsoft 数据访问组件的未来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 而是使用驱动程序和服务器游标。  
  
 ODBC 游标库除了[在 ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)中列出的 SQLSTAT 外，还返回以下 SQLSTAT。  
  
> [!NOTE]  
>  游标库不排序状态记录;因此，游标库不对状态记录进行排序。驱动程序管理器和 ODBC 3。*x*驱动程序负责订购状态记录。  
  
|SQLSTATE|描述|可以从|  
|--------------|-----------------|--------------------------|  
|01000|光标不可上用。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|不使用光标库。 加载失败。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用光标库。 驱动程序支持不足。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用光标库。 版本与驱动程序管理器不匹配。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|驱动程序返回SQL_SUCCESS_WITH_INFO。 警告消息已丢失。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|一般错误：无法创建文件缓冲区。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般错误：无法从文件缓冲区读取。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般错误：无法写入文件缓冲区。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般错误：无法关闭或删除文件缓冲区。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|无法执行定位请求，因为未绑定任何可搜索列。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|无法执行定位请求，因为结果集由联接条件创建。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|绑定缓冲区超过最大段大小。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|结果集不是由**SELECT**语句生成的。|**SQLGetData**|  
|SL005|**SELECT**语句包含一个 GROUP BY 子句。|**SQLGetData**|  
|SL006|定位请求不支持参数数组。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData**不允许在仅转发（非缓冲）游标上。|**SQLGetData**|  
|SL009|在调用**SQLFetch**或**SQLFetchScroll**之前，没有绑定任何列。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|在尝试绑定到内部缓冲区期间 **，SQLBindCol**返回SQL_ERROR。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|语句选项仅在调用**SQLFetch**或**SQLFetchScroll**后才有效。|**SQLGetStmtAttr**|  
|SL012|打开游标时，不能更改语句绑定。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|已发出定位请求，并且并非所有列计数字段都进行了缓冲。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch**和**SQLFetchScroll**不能混合。|**SQL 扩展获取**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
