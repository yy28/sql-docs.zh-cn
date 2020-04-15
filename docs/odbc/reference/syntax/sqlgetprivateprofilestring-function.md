---
title: SQLGet 私人配置文件字符串功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c12fc8d08535960cbb239c14e017b2ad5faa6c0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303289"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函数
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **SQLGetPrivateProfileString**获取与系统信息值对应的值或数据的名称列表。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>参数  
 *lpsz节*  
 [输入]指向指定包含键名称的节的 null 端接字符串。 如果此参数为 NULL，则函数将文件中的所有节名称复制到提供的缓冲区。  
  
 *lpszEntry*  
 [输入]指向包含要检索其关联字符串的键名称的 null 终止字符串。 如果此参数为 NULL，*则 lpszSection*参数指定的节中的所有键名都将复制到*RetBuffer*参数指定的缓冲区。  
  
 *lpszDefault*  
 [输入]指向一个 null 端接字符串，该字符串指定给定键的默认值，如果在初始化文件中找不到该键。 此参数不能为 NULL。  
  
 *RetBuffer*  
 [输出]指向接收检索的字符串的缓冲区。  
  
 *cbRetBuffer*  
 [输入]指定*RetBuffer*参数指向的缓冲区的大小（以字符表示）。  
  
 *lpszFile名称*  
 [输入]指向命名初始化文件的 null 终止字符串。 如果此参数不包含文件的完整路径，则搜索默认目录。  
  
## <a name="returns"></a>返回  
 **SQLGetPrivateProfileString**返回一个整数值，指示读取的字符数。  
  
## <a name="diagnostics"></a>诊断  
 当对**SQLGetPrivateProfileString**的调用失败时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLGetPrivateProfileString**作为将驱动程序和驱动程序设置 DLL 从 Microsoft ® Windows ® 移植到 Microsoft Windows NT®/Windows 2000 的简单方法提供。 从 Odbc.ini 文件中检索配置文件字符串的**GetPrivateProfileString**的调用应替换为对**SQLGetPrivateProfileString**的调用。 **SQLGetPrivateProfileString**调用 Win32® API 中的函数来检索与系统信息 Odbc.ini 子键的值对应的值或数据的请求名称。  
  
 配置模式（由**SQLSetConfigMode**设置）指示 Odbc.ini 条目列表 DSN 值在系统信息中的位置。 如果 DSN 是用户 DSN（配置模式USERDSN_ONLY），则函数将从 HKEY_CURRENT_USER 中的 Odbc.ini 条目读取。 如果 DSN 是系统 DSN（SYSTEMDSN_ONLY），则函数将从 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目读取。 如果配置模式为 BOTHDSN，则尝试HKEY_CURRENT_USER，如果配置模式失败，则使用HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|向系统信息写入值|[SQLWrite 私有配置文件字符串](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
