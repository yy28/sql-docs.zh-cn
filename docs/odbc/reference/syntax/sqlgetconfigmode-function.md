---
title: SQLGetConfigMode 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 397f4ef5a2efd8e663544f5e21171c2184db1b30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917242"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLGetConfigMode**检索配置模式下，该值指示系统信息中列出 DSN 值 Odbc.ini 该项，则其中。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>参数  
 *pwConfigMode*  
 [输出]指向包含将配置模式的缓冲区的指针。 （请参阅"注释"。）中的值 *\*pwConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetConfigMode**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 此函数用于确定列出 DSN 值 Odbc.ini 条目中的系统信息的位置。 如果 *\*pwConfigMode* ODBC_USER_DSN，DSN 为用户 DSN，此函数将读取从中 HKEY_CURRENT_USER 的 Odbc.ini 条目。 如果它是 ODBC_SYSTEM_DSN，DSN 是系统 DSN 和此函数将读取从中 HKEY_LOCAL_MACHINE 的 Odbc.ini 条目。 如果它是 ODBC_BOTH_DSN，会尝试 HKEY_CURRENT_USER，并且如果失败，HKEY_LOCAL_MACHINE 适用。  
  
 默认情况下， **SQLGetConfigMode**返回 ODBC_BOTH_DSN。 通过调用创建用户 DSN 或系统 DSN 是**SQLConfigDataSource**，该函数将配置模式设置为 ODBC_USER_DSN 或 ODBC_SYSTEM_DSN 来修改 DSN 时区分用户和系统 Dsn。 在返回前, **SQLConfigDataSource**将配置模式下重置为 ODBC_BOTH_DSN。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|设置配置模式|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
