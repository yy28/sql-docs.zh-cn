---
title: ODBC 游标库错误代码 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fb86e1332e3b7e4d89003ccf6421151e5d9cec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100672"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC 游标库错误代码
> [!IMPORTANT]  
>  Microsoft 数据访问组件的未来版本中，将删除此功能。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 相反，使用驱动程序和服务器游标。  
  
 ODBC 游标库返回除了所列出的以下 SQLSTATEs [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
> [!NOTE]  
>  游标库不排序状态记录;驱动程序管理器和 ODBC 3。*x*驱动程序负责排序状态记录。  
  
|SQLSTATE|描述|可以从返回|  
|--------------|-----------------|--------------------------|  
|01000|游标是不可更新。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|不使用游标库。 加载失败。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用游标库。 没有足够的驱动程序支持。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|不使用游标库。 版本不匹配的驱动程序管理器。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|驱动程序返回 SQL_SUCCESS_WITH_INFO。 警告消息已丢失。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|常规错误：无法创建文件缓冲区。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|常规错误：无法从文件缓冲区中读取。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|常规错误：无法写入文件缓冲区。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|常规错误：无法关闭或删除文件缓冲区。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|不能执行定位的请求，因为没有可搜索的列绑定。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|无法执行定位的请求，因为联接条件创建结果集。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|绑定的缓冲区超出了最大段大小。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|通过不生成结果集**选择**语句。|**SQLGetData**|  
|SL005|**选择**语句包含 GROUP BY 子句。|**SQLGetData**|  
|SL006|参数数组不支持定位请求。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData**不允许对只进的 （非缓冲） 游标。|**SQLGetData**|  
|SL009|没有列绑定之前调用**SQLFetch**或**SQLFetchScroll**。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol**期间尝试绑定到的内部缓冲区返回 SQL_ERROR。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|语句选项仅在调用后才有效**SQLFetch**或**SQLFetchScroll**。|**SQLGetStmtAttr**|  
|SL012|打开游标时，不能更改语句绑定。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|发出定位的请求，并不是所有的列计数字段已缓冲处理。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch**并**SQLFetchScroll**不能混合。|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
