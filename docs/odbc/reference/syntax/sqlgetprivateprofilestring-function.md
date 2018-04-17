---
title: SQLGetPrivateProfileString 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e970b4d3e087e2df4043a36f1fe2881680cf7d3b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函数
**一致性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **SQLGetPrivateProfileString**获取的值或数据的系统信息值相应的名称的列表。  
  
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
 [输入]指向以 null 结尾的字符串，指定包含密钥名称的部分。 如果此参数为 NULL，函数将复制所有的部分名称在文件中到提供的缓冲区。  
  
 *lpszEntry*  
 [输入]指向以 null 结尾的字符串，包含其关联的字符串是要检索的密钥名称。 如果此参数为 NULL，所有密钥名称的指定段中*lpszSection*自变量复制到指定的缓冲区*RetBuffer*自变量。  
  
 *lpszDefault*  
 [输入]指向以 null 结尾的字符串，以指定给定键的默认值，如果在初始化文件中找不到键。 此参数不能为 NULL。  
  
 *RetBuffer*  
 [输出]指向接收检索到的字符串的缓冲区。  
  
 *cbRetBuffer*  
 [输入]以字符为单位，指向缓冲区的指定的大小， *RetBuffer*自变量。  
  
 *lpszFilename*  
 [输入]指向以 null 结尾的名称初始化文件的字符串。 如果此参数不包含文件的完整路径，则搜索默认目录。  
  
## <a name="returns"></a>返回  
 **SQLGetPrivateProfileString**返回一个整数值，该值指示读取的字符数。  
  
## <a name="diagnostics"></a>诊断  
 当调用**SQLGetPrivateProfileString**失败，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLGetPrivateProfileString**作为一种简单方法端口驱动程序和驱动程序安装程序 Dll 从 Microsoft® Windows® 提供给 Microsoft Windows/Windows 2000。 调用**GetPrivateProfileString** Odbc.ini 文件从一个配置文件字符串应使用替换该检索调用**SQLGetPrivateProfileString**。 **SQLGetPrivateProfileString**中要检索请求的名称值或数据的系统信息的 Odbc.ini 子项值相对应的 Win32® API 调用函数。  
  
 将配置模式 (通过设置，如同**SQLSetConfigMode**) 指示列出 DSN 值的 Odbc.ini 项所在的系统信息。 如果 DSN （将配置模式是 USERDSN_ONLY） 用户 DSN，则此函数将读取从中 HKEY_CURRENT_USER 的 Odbc.ini 条目。 如果 DSN 系统 DSN (SYSTEMDSN_ONLY)，此函数将读取从中 HKEY_LOCAL_MACHINE 的 Odbc.ini 条目。 如果将配置模式，BOTHDSN HKEY_CURRENT_USER 尝试，并且如果失败，HKEY_LOCAL_MACHINE 适用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|一个值写入的系统信息|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
