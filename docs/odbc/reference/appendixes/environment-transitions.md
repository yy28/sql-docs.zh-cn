---
title: 环境转换 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ed2bbf40ac333db34d3920b2ed2ec688c344bfe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188985"
---
# <a name="environment-transitions"></a>环境转换
ODBC 环境具有以下三种状态。  
  
|State|描述|  
|-----------|-----------------|  
|E0|未分配的环境|  
|E1|分配的环境中，未分配的连接|  
|E2|分配环境中，分配连接|  
  
 下表显示每个 ODBC 函数如何影响环境状态。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|E1[1]|--[4]|--[4]|  
|(IH)[2]|E2[5]<br />(HY010)[6]|--[4]|  
|(IH)[3]|(IH)|--[4]|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 此行显示转换时*HandleType*为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 调用**SQLAllocHandle**与*OutputHandlePtr*指向有效的句柄将覆盖该句柄。 这可能是应用程序的编程错误。  
  
 [在环境中设置 5] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [不在环境中设置 6] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1] 的 SQL_ATTR_ODBC_VERSION 环境属性设置为环境。  
  
 [2] 的 SQL_ATTR_ODBC_VERSION 环境属性不在环境中设置。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(IH)[2]|(IH)|--|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [在环境中设置 3] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
 [不在环境中设置 4] 的 SQL_ATTR_ODBC_VERSION 环境属性。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|E0|(HY010)|  
|(IH)[2]|(IH)|--[4]<br />E1[5]|  
|(IH)[3]|(IH)|--|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*已 SQL_HANDLE_DBC。  
  
 [3] 此行显示转换时*HandleType*为 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
 [4] 没有其他已分配的连接句柄。  
  
 [5] 中指定的连接句柄*处理*是唯一的已分配的连接句柄。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)[1]|--|--|  
|(IH)[2]|(IH)|--|  
  
 [1] 此行显示转换时*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 此行显示转换时*HandleType*为 SQL_HANDLE_DBC、 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|--|  
  
 [1] 的 SQL_ATTR_ODBC_VERSION 环境属性设置为环境。  
  
 [2] 的 SQL_ATTR_ODBC_VERSION 环境属性不在环境中设置。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|--[1]<br />(HY010)[2]|（HY011 并显示）|  
  
 [1] 的 SQL_ATTR_ODBC_VERSION 环境属性设置为环境。  
  
 [2]*特性*参数不为 SQL_ATTR_ODBC_VERSION，并且 SQL_ATTR_ODBC_VERSION 环境属性具有未在环境中设置。  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函数  
  
|E0<br /><br /> 未分配|E1<br /><br /> 分配|E2<br /><br /> 连接|  
|------------------------|----------------------|-----------------------|  
|(IH)|(IH)|--|
