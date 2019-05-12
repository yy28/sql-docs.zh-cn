---
title: SQLWritePrivateProfileString 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff853976cf0d900cb24391ff6bf13838782ea876
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536768"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函数
**符合性**  
 版本引入了：ODBC 2.0  
  
 **摘要**  
 **SQLWritePrivateProfileString**将值名称和数据写入到的系统信息的 Odbc.ini 子项。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>参数  
 *lpszSection*  
 [输入]指向包含该字符串将复制到其中的部分的名称的以 null 结尾的字符串。 如果该节不存在，则创建它。 节的名称与用例无关;字符串可以是任何组合的大写和小写字母。  
  
 *lpszEntry*  
 [输入]指向以 null 终止的字符串包含与字符串相关联的密钥的名称。 如果键不存在指定的节中，将创建它。 如果此参数为 NULL，则将删除整个节，其中包括部分内的所有条目。  
  
 *lpszString*  
 [输入]指向以 null 结尾的字符串写入到文件。 如果此参数为 NULL，该密钥由指向*lpszEntry*删除参数。  
  
 *lpszFilename*  
 [输出]指向以 null 结尾的名称初始化文件的字符串。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWritePrivateProfileString**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|无法写入请求的系统信息。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLWritePrivateProfileString**到 Microsoft Windows/Windows 2000 提供为端口驱动程序和驱动程序安装程序 Dll 从 Microsoft® Windows® 的简单方式。 调用**WritePrivateProfileString**的写入 Odbc.ini 文件的配置文件字符串应替换为对调用**SQLWritePrivateProfileString**。 **SQLWritePrivateProfileString** Win32® API 将指定的值名称和数据添加到系统信息的 Odbc.ini 子项中调用函数。  
  
 配置模式指示列出 DSN 的值的 Odbc.ini 项所在的系统信息中。 如果在 DSN 是用户 DSN （状态变量是 USERDSN_ONLY），该函数将写入到 HKEY_CURRENT_USER 中的 Odbc.ini 条目。 如果在 DSN 是系统 DSN (SYSTEMDSN_ONLY)，该函数将写入到 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目。 如果状态变量，BOTHDSN 尝试 HKEY_CURRENT_USER 和 HKEY_LOCAL_MACHINE 如果失败，则使用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取一个值中的系统信息|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
