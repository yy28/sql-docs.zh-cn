---
title: SQLSet 配置模式功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293277"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLSetConfigMode**设置配置模式，指示 Odbc.ini 条目列表 DSN 值在系统信息中的位置。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>参数  
 *w 配置模式*  
 [输入]安装程序配置模式（请参阅"注释"）。 *wConfigMode*中的值可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLSetConfigMode**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效参数序列|*wConfigMode*参数不包含ODBC_USER_DSN、ODBC_SYSTEM_DSN 或ODBC_BOTH_DSN。|  
  
## <a name="comments"></a>注释  
 此功能用于设置 Odbc.ini 条目列表 DSN 值在系统信息中的位置。 如果*wConfigMode* ODBC_USER_DSN，则 DSN 是用户 DSN，函数从 odbc.ini 条目读取HKEY_CURRENT_USER。 如果ODBC_SYSTEM_DSN，DSN 是系统 DSN，函数从 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目读取。 如果ODBC_BOTH_DSN，则尝试HKEY_CURRENT_USER，如果失败，则使用HKEY_LOCAL_MACHINE。  
  
 此函数不影响**SQLCreateDataSource**和**SQLDriverConnect**。 当驱动程序通过调用**SQLGetPrivateProfileString**或通过调用**SQLWritePrivateProfileString**从注册表读取时，必须设置配置模式。 对**SQLGetPrivateProfileString**和**SQLWritePrivateProfileString**的调用使用配置模式来了解要操作的注册表的哪个部分。  
  
> [!CAUTION]  
>  仅在必要时才应调用**SQLSet 配置模式**;如果模式设置不正确，ODBC 安装程序可能无法正常运行。  
  
 **SQLSetConfigMode**对配置模式进行直接注册表修改。 这与通过调用**SQLConfigDataSource**修改配置模式的过程不同。 对**SQLConfigDataSource**的调用将配置模式设置在修改 DSN 时区分用户和系统 DSN。 在返回之前 **，SQLConfigDataSource**会将配置模式重置为 BOTHDSN。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|创建数据源|[SQLCreate数据源](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|检索配置模式|[SQLGet 配置模式](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
