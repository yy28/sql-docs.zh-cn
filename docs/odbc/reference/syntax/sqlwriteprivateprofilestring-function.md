---
title: SQLWrite 私人配置文件字符串功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286880"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函数
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **SQLWritePrivateProfileString**将值名称和数据写入系统信息的 Odbc.ini 子键。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>参数  
 *lpsz节*  
 [输入]指向包含要复制该字符串的节的名称的 null 终止字符串。 如果节不存在，则创建该节。 该节的名称与案例无关;字符串可以是大写字母和小写字母的任意组合。  
  
 *lpszEntry*  
 [输入]指向包含要与字符串关联的键名称的 null 端接字符串。 如果该键在指定的节中不存在，则创建该键。 如果此参数为 NULL，则删除整个节，包括节中的所有条目。  
  
 *lpszString*  
 [输入]指向要写入文件的 null 终止字符串。 如果此参数为 NULL，则删除*lpszEntry*参数指向的键。  
  
 *lpszFile名称*  
 [输出]指向命名初始化文件的 null 终止字符串。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWritePrivateProfileString**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_REQUEST_FAILED|申请失败。|无法写入请求的系统信息。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLWritePrivateProfileString**作为将驱动程序和驱动程序设置 DLL 从 Microsoft ® Windows ® 移植到 Microsoft Windows NT®/Windows 2000 的简单方法提供。 对**写入私有配置文件String**的调用，将配置文件字符串写入 Odbc.ini 文件应替换为对**SQLWritePrivateProfileString**的调用。 **SQLWritePrivateProfileString**调用 Win32® API 中的函数，将指定的值名称和数据添加到系统信息的 Odbc.ini 子键。  
  
 配置模式指示 Odbc.ini 条目列表 DSN 值在系统信息中的位置。 如果 DSN 是用户 DSN（状态变量为USERDSN_ONLY），则函数将写入 HKEY_CURRENT_USER 中的 Odbc.ini 条目。 如果 DSN 是系统 DSN （SYSTEMDSN_ONLY），则函数将写入 HKEY_LOCAL_MACHINE 中的 Odbc.ini 条目。 如果状态变量为 BOTHDSN，则尝试HKEY_CURRENT_USER，如果失败，则使用HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|从系统信息获取值|[SQLGet 私人配置文件字符串](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
