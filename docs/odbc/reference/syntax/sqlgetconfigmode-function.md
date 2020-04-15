---
title: SQLGet 配置模式功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc11bec24ede3352dd43f3645fb8c720b77fdabe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285687"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLGetConfigMode**检索指示 Odbc.ini 条目列表 DSN 值在系统信息中的位置的配置模式。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>参数  
 *pwConfigmode*  
 [输出]指向包含配置模式的缓冲区的指针。 （请参阅"注释"。* \*pwConfigMode*中的值可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetConfigMode**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 此功能用于确定 Odbc.ini 条目列表 DSN 值在系统信息中的位置。 如果*\*pwConfigMode* ODBC_USER_DSN，则 DSN 是用户 DSN，函数从 HKEY_CURRENT_USER 中的 Odbc.ini 条目读取。 如果ODBC_SYSTEM_DSN，DSN 是系统 DSN，函数从 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目读取。 如果ODBC_BOTH_DSN，则尝试HKEY_CURRENT_USER，如果失败，则使用HKEY_LOCAL_MACHINE。  
  
 默认情况下 **，SQLGet ConfigMode**返回ODBC_BOTH_DSN。 当用户 DSN 或系统 DSN 通过调用**SQLConfigDataSource**创建时，该函数将配置模式设置为ODBC_USER_DSN或ODBC_SYSTEM_DSN，以在修改 DSN 时区分用户和系统 DSN。 在返回之前 **，SQLConfigDataSource**会将配置模式重置为ODBC_BOTH_DSN。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|设置配置模式|[SQLSet 配置模式](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
