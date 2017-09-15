---
title: "SQLWritePrivateProfileString 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3025fedee1c5528704c366fa04c5d7ff32e124ee
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函数
**一致性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **SQLWritePrivateProfileString**写入的系统信息的 Odbc.ini 子项的值名称和数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>参数  
 *lpszSection*  
 [输入]指向以 null 结尾的字符串包含名称的字符串将复制到其中的部分。 如果该节不存在，则创建它。 节的名称是独立于; 的大小写的字符串可以是任何组合的大写和小写字母。  
  
 *lpszEntry*  
 [输入]指向以 null 结尾的字符串包含要与字符串相关联的密钥的名称。 如果键不存在于指定的节，则创建它。 如果此参数为 NULL，将删除整个部分中，包括在部分中，所有条目。  
  
 *lpszString*  
 [输入]指向以 null 结尾的字符串写入到文件。 如果此参数为 NULL，该密钥的指向*lpszEntry*删除自变量。  
  
 *lpszFilename*  
 [输出]指向以 null 结尾的名称初始化文件的字符串。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWritePrivateProfileString**返回 FALSE，一个关联* \*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出* \*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|无法写入请求的系统信息。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLWritePrivateProfileString**作为一种简单方法端口驱动程序和驱动程序安装程序 Dll 从 Microsoft® Windows® 提供给 Microsoft Windows/Windows 2000。 调用**WritePrivateProfileString**编写 Odbc.ini 文件的配置文件字符串应使用对的调用替换**SQLWritePrivateProfileString**。 **SQLWritePrivateProfileString** Win32® API，将指定的值名称和数据添加到的系统信息的 Odbc.ini 子项中调用函数。  
  
 配置模式指示列出 DSN 值的 Odbc.ini 项所在的系统信息。 如果 DSN （状态变量是 USERDSN_ONLY） 用户 DSN，该函数将写入中 HKEY_CURRENT_USER 的 Odbc.ini 条目。 如果 DSN 系统 DSN (SYSTEMDSN_ONLY)，该函数将写入中 HKEY_LOCAL_MACHINE 的 Odbc.ini 条目。 如果状态变量，BOTHDSN HKEY_CURRENT_USER 尝试，并且如果失败，HKEY_LOCAL_MACHINE 适用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|从系统信息中获取一个值|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
