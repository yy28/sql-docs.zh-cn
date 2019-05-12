---
title: SQLGetConfigMode Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d9065d48e8b4af686e1ff64272fbe902e066cb6
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537277"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函数
**符合性**  
 版本引入了：ODBC 3.0  
  
 **摘要**  
 **SQLGetConfigMode**检索指示列出 DSN 的值的 Odbc.ini 项所在的系统信息中的配置模式。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>参数  
 *pwConfigMode*  
 [输出]指向包含配置模式下的缓冲区的指针。 （请参阅"注释"。）中的值 *\*pwConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetConfigMode**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 此函数用于确定列出 DSN 的值的 Odbc.ini 条目中的系统信息的位置。 如果 *\*pwConfigMode* ODBC_USER_DSN，DSN 是一个用户 DSN 和此函数将读取从 HKEY_CURRENT_USER 中的 Odbc.ini 条目。 如果 ODBC_SYSTEM_DSN，DSN 是系统 DSN，此函数将读取从 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目。 如果它是 ODBC_BOTH_DSN，尝试 HKEY_CURRENT_USER 和 HKEY_LOCAL_MACHINE 如果失败，则使用。  
  
 默认情况下**SQLGetConfigMode**返回 ODBC_BOTH_DSN。 当通过调用创建一个用户 DSN 或系统 DSN **SQLConfigDataSource**，该函数将配置模式设置为 ODBC_USER_DSN 或 ODBC_SYSTEM_DSN 来修改 DSN 时区分用户和系统 Dsn。 在返回前, **SQLConfigDataSource**将配置模式下重置为 ODBC_BOTH_DSN。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|设置配置模式|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
