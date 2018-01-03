---
title: "环境转换 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a47acf216ef707600fad3fd28a8d94603052be6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="environment-transitions"></a>环境转换
ODBC 环境具有以下三种状态。  
  
|State|Description|  
|-----------|-----------------|  
|E0|未分配的环境|  
|E1|已分配的环境，未分配的连接|  
|E2|分配分配连接的环境|  
  
 下表显示每个 ODBC 函数如何影响环境状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(IH)[2]|E2 [5]<br />(HY010)[6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 该行显示转换时*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 调用**SQLAllocHandle**与*OutputHandlePtr*指向有效的句柄将覆盖该句柄。 这可能是一个应用程序的编程错误。  
  
 [已在环境上设置 5] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [不在环境上设 6] SQL_ATTR_ODBC_VERSION 环境属性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [已在环境上设置 1] SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [2] 上，SQL_ATTR_ODBC_VERSION 环境属性必须在环境尚未设置。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [已在环境上设置 3] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [不在环境上设 4] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1 [5]|  
|(IH)[3]|(IH)|--|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 该行显示转换时*HandleType* SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 没有其他分配的连接句柄。  
  
 [指定在 5] 的连接句柄*处理*是唯一的已分配的连接句柄。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1] 该行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 该行显示转换时*HandleType* SQL_HANDLE_DBC、 SQL_HANDLE_STMT，或 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [已在环境上设置 1] SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [2] 上，SQL_ATTR_ODBC_VERSION 环境属性必须在环境尚未设置。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [已在环境上设置 1] SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [2]*属性*自变量不 SQL_ATTR_ODBC_VERSION，而且 SQL_ATTR_ODBC_VERSION 环境属性具有未在环境中设置。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函数  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
