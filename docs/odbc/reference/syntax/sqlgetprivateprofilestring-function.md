---
title: 不到 SQLGetPrivateProfileString 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77d1f433732cf710e715418df94eba5184e9a907
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210126"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函数
**符合性**  
 版本引入了：ODBC 2.0  
  
 **摘要**  
 **不到 SQLGetPrivateProfileString**获取一系列的值或数据的系统信息值对应的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>参数  
 *lpszSection*  
 [输入]指向一个以 null 结尾的字符串，指定包含密钥名称的部分。 如果此参数为 NULL，函数将复制所有的部分名称在文件中为所提供的缓冲区。  
  
 *lpszEntry*  
 [输入]指向包含其关联的字符串是要检索的键名的以 null 结尾的字符串。 如果此参数为 NULL，所有在密钥中指定的节的名称*lpszSection*自变量复制到指定的缓冲区*RetBuffer*参数。  
  
 *lpszDefault*  
 [输入]指向以 null 终止的字符串，如果在初始化文件中找不到键指定的默认值为给定的键。 此参数不能为 NULL。  
  
 *RetBuffer*  
 [输出]指向接收检索到的字符串的缓冲区。  
  
 *cbRetBuffer*  
 [输入]指定的大小，以字符为单位通过指向的缓冲区*RetBuffer*参数。  
  
 *lpszFilename*  
 [输入]指向以 null 结尾的名称初始化文件的字符串。 如果此参数不包含该文件的完整路径，则搜索默认目录。  
  
## <a name="returns"></a>返回  
 **不到 SQLGetPrivateProfileString**返回一个整数值，该值指示读取的字符数。  
  
## <a name="diagnostics"></a>诊断  
 在调用**SQLGetPrivateProfileString**失败，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **不到 SQLGetPrivateProfileString**到 Microsoft Windows/Windows 2000 提供为端口驱动程序和驱动程序安装程序 Dll 从 Microsoft® Windows® 的简单方式。 调用**GetPrivateProfileString**调用中的 Odbc.ini 文件的配置文件字符串应替换为该检索**SQLGetPrivateProfileString**。 **不到 SQLGetPrivateProfileString**中要检索的值或系统信息的 Odbc.ini 子项的值对应的数据请求的名称的 Win32® API 调用的函数。  
  
 配置模式 (通过设置**SQLSetConfigMode**) 指示列出 DSN 的值的 Odbc.ini 项所在的系统信息中。 如果在 DSN 是用户 DSN （配置模式是 USERDSN_ONLY），该函数将读取从 HKEY_CURRENT_USER 中的 Odbc.ini 条目。 如果在 DSN 是系统 DSN (SYSTEMDSN_ONLY)，该函数将读取从 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目。 如果配置模式下，BOTHDSN 尝试 HKEY_CURRENT_USER 和 HKEY_LOCAL_MACHINE 如果失败，则使用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|一个值写入系统信息|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
