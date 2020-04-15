---
title: 环境转换 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebfb5475d24d5fc70c4cb46a666b2573066565a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283297"
---
# <a name="environment-transitions"></a>环境转换
ODBC 环境具有以下三种状态。  
  
|状态|描述|  
|-----------|-----------------|  
|E0|未分配的环境|  
|E1|已分配的环境，未分配的连接|  
|E2|已分配的环境，已分配的连接|  
  
 下表显示了每个 ODBC 函数如何影响环境状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|（IH）[2]|E2[5]<br />（HY010）[6]|--[4]|  
|（IH）[3]|（IH）|--[4]|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV时的过渡。  
  
 [2] 此行显示*HandleType* SQL_HANDLE_DBC时的过渡。  
  
 [3] 此行显示*HandleType* SQL_HANDLE_STMT或SQL_HANDLE_DESC时的过渡。  
  
 [4] 使用*OutputHandlePtr*调用**SQLAllocHandle，** 指向有效的句柄覆盖该句柄。 这可能是应用程序编程错误。  
  
 [5] SQL_ATTR_ODBC_VERSION环境属性已设置在环境中。  
  
 [6] 未在环境中设置SQL_ATTR_ODBC_VERSION环境属性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLData 源和 SQL 驱动程序  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）|--[1]<br />（HY010）[2]|--[1]<br />（HY010）[2]|  
  
 [1] SQL_ATTR_ODBC_VERSION环境属性已设置在环境中。  
  
 [2] 未在环境中设置SQL_ATTR_ODBC_VERSION环境属性。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）[1]|--[3]<br />（HY010）[4]|--[3]<br />（HY010）[4]|  
|（IH）[2]|（IH）|--|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV时的过渡。  
  
 [2] 此行显示*HandleType* SQL_HANDLE_DBC时的过渡。  
  
 [3] SQL_ATTR_ODBC_VERSION环境属性已设置在环境中。  
  
 [4] 未在环境中设置SQL_ATTR_ODBC_VERSION环境属性。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）[1]|E0|（HY010）|  
|（IH）[2]|（IH）|--[4]<br />E1[5]|  
|（IH）[3]|（IH）|--|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV时的过渡。  
  
 [2] 此行显示*HandleType* SQL_HANDLE_DBC时的过渡。  
  
 [3] 此行显示*HandleType* SQL_HANDLE_STMT或SQL_HANDLE_DESC时的过渡。  
  
 [4] 还有其他已分配的连接句柄。  
  
 [5]*在句柄*中指定的连接句柄是唯一分配的连接句柄。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）[1]|--|--|  
|（IH）[2]|（IH）|--|  
  
 [1] 此行显示*HandleType* SQL_HANDLE_ENV时的过渡。  
  
 [2] 此行显示*HandleType* SQL_HANDLE_DBC、SQL_HANDLE_STMT 或SQL_HANDLE_DESC时的过渡。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）|--[1]<br />（HY010）[2]|--|  
  
 [1] SQL_ATTR_ODBC_VERSION环境属性已设置在环境中。  
  
 [2] 未在环境中设置SQL_ATTR_ODBC_VERSION环境属性。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）|--[1]<br />（HY010）[2]|（HY011）|  
  
 [1] SQL_ATTR_ODBC_VERSION环境属性已设置在环境中。  
  
 [2]*属性*参数未SQL_ATTR_ODBC_VERSION，并且未在环境中设置SQL_ATTR_ODBC_VERSION环境属性。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 功能  
  
|E0<br /><br /> 未分配|E1<br /><br /> 已分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|（IH）|（IH）|--|
