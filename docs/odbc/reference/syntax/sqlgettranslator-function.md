---
title: SQLGet 翻译器功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcd5aeebab8539b8b94db56ff30892f4a7dbbac1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303268"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函数
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **SQLGet 转换器**显示一个对话框，用户可以从该对话框中选择译员。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd 家长*  
 [输入]父窗口句柄。  
  
 *lpsz名称*  
 [输入/输出]系统信息中的转换器名称。  
  
 *cbNameMax*  
 [输入]*lpszName*缓冲区的最大长度。  
  
 *pcbNameOut*  
 [输入/输出]以*lpszName*通过或返回的字节总数（不包括空终止字节）。 如果可用于返回的字节数大于或等于*cbNameMax，**则 lpszName*中的转换器名称将被截断为*cbNameMax*减去 null 终止字符。 *pcbNameOut*参数可以是空指针。  
  
 *lpszPath*  
 [输出]翻译 DLL 的完整路径。  
  
 *cbPathMax*  
 [输入]*lpszPath*缓冲区的最大长度。  
  
 *多巴帕路*  
 [输出]在*lpszPath*中返回的字节总数（不包括空终止字节）。 如果可用于返回的字节数大于或等于*cbPathMax，**则 lpszPath*中的转换 DLL 路径将截断为*cbPathMax*减去 null 终止字符。 *pcbPathOut*参数可以是空指针。  
  
 *pvOption*  
 [输出] 32 位转换选项。  
  
## <a name="returns"></a>返回  
 如果成功，则函数将返回 TRUE;如果失败或用户取消对话框，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGet 转换器**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*cbNameMax*或*cbPathMax*参数小于或等于 0。|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd 父参数*无效或 NULL。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszName*参数无效。 在注册表中找不到它。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器设置库|无法加载转换器库。|  
|ODBC_ERROR_INVALID_OPTION|无效事务选项|*pvOption*参数包含无效值。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 如果*hwndParent*为空，或者如果*lpszName、lpszPath*或*pvOption*是空指针，**则 SQLGet 转换器**返回 FALSE。 *lpszPath* 否则，它将在下面的对话框中显示已安装的译员的列表。  
  
 ![“选择转换器”对话框](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果*lpszName*包含有效的转换器名称，则选中该名称。 否则，\<则不选择"翻译>。  
  
 \<如果用户选择"无翻译器>，则不会触摸*lpszName、lpszPath*和*pvOption*的内容。 *lpszPath* **SQLGet 转换器**将*pcbNameOut*和*pcbPathOut*设置为 0，并返回 TRUE。  
  
 如果用户选择翻译**器，SQLGet 转换器**在译员的设置 DLL 中调用**配置翻译器**。 如果**配置转换器**返回**FALSE，SQLGet 转换器**将返回到其对话框。 如果**配置转换器**返回**TRUE，SQLGet 转换器**将返回 TRUE，以及所选的转换器名称、路径和翻译选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|配置译员|[配置转换器](../../../odbc/reference/syntax/configtranslator-function.md)|  
|获取翻译属性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|设置转换属性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
