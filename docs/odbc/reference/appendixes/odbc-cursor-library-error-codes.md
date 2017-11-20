---
title: "ODBC 游标库错误代码 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 308ad8ed54aacb9ab7bc169efd9dad020e2f2b66
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 游标库错误代码
> [!IMPORTANT]  
>  Microsoft 数据访问组件的未来版本中，将删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 相反，使用驱动程序和服务器游标。  
  
 ODBC 游标库返回除中列出以下 SQLSTATEs [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
> [!NOTE]  
>  游标库不排序状态记录。驱动程序管理器和 ODBC 3。*x*驱动程序负责排序状态记录。  
  
|SQLSTATE|Description|可以从返回|  
|--------------|-----------------|--------------------------|  
|01000|游标不是可更新的。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|未使用的游标库。 加载失败。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|未使用的游标库。 没有足够的驱动程序支持。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|未使用的游标库。 版本不匹配与驱动程序管理器。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|驱动程序返回 SQL_SUCCESS_WITH_INFO。 警告消息已丢失。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|常规错误： 无法创建文件缓冲区。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|常规错误： 无法从文件缓冲区读取。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|常规错误： 无法写入文件缓冲区。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|常规错误： 无法关闭或删除文件缓冲区。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|无法执行定位的请求，因为没有可搜索的列绑定。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|无法执行定位的请求，因为结果集由联接条件。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|绑定的缓冲区超出最大的段大小。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|结果集不生成通过**选择**语句。|**SQLGetData**|  
|SL005|**选择**语句包含 GROUP BY 子句。|**SQLGetData**|  
|SL006|参数数组不支持定位请求。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData**上只进的 （非缓冲） 游标不允许。|**SQLGetData**|  
|SL009|没有列绑定之前调用**SQLFetch**或**SQLFetchScroll**。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol**返回 SQL_ERROR 在尝试将绑定到的内部缓冲区的过程。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|仅在调用之后的语句选项才有效**SQLFetch**或**SQLFetchScroll**。|**SQLGetStmtAttr**|  
|SL012|打开游标时，不能更改语句绑定。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|发出定位的请求，并不是所有的列计数字段已缓冲处理。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch**和**SQLFetchScroll**不能混合。|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|

