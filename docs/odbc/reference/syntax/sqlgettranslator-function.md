---
title: SQLGetTranslator 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1f1c5bbfd2e2fbf91fd9e91acafe0bc72d006d3f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209316"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函数
**符合性**  
 版本引入了：ODBC 2.0  
  
 **摘要**  
 **SQLGetTranslator**显示一个对话框，用户可以从中选择转换器。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 *hwndParent*  
 [输入]父窗口句柄。  
  
 *lpszName*  
 [输入/输出]系统信息从转换器的名称。  
  
 *cbNameMax*  
 [输入]最大长度*lpszName*缓冲区。  
  
 *pcbNameOut*  
 [输入/输出]（不包括 null 终止字节） 的字节总数传递或返回*lpszName*。 可用来返回的字节数是否大于或等于*cbNameMax*中的转换器名称*lpszName*将被截断为*cbNameMax*减null 终止字符。 *PcbNameOut*参数可以是 null 指针。  
  
 *lpszPath*  
 [输出]转换 DLL 的完整路径。  
  
 *cbPathMax*  
 [输入]最大长度*lpszPath*缓冲区。  
  
 *pcbPathOut*  
 [输出]总字节数 （不包括 null 终止字节） 中返回*lpszPath*。 可用来返回的字节数是否大于或等于*cbPathMax*中的转换 DLL 路径*lpszPath*将被截断为*cbPathMax*减null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
 *pvOption*  
 [输出] 32 位转换选项。  
  
## <a name="returns"></a>返回  
 如果它是成功，则为 FALSE 或失败时如果用户取消了对话框中，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetTranslator**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效缓冲区长度|*CbNameMax*或*cbPathMax*参数为小于或等于 0。|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*参数为无效或为 NULL。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszName*参数无效。 它找不到注册表中。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装程序库|无法加载翻译库。|  
|ODBC_ERROR_INVALID_OPTION|无效的事务选项|*PvOption*参数包含无效的值。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 如果*hwndParent*为 null 或者如果*lpszName*， *lpszPath*，或者*pvOption*是 null 指针， **SQLGetTranslator**方法将返回 FALSE。 否则，在下列对话框中显示已安装的转换器的列表。  
  
 ![选择转换器对话框](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果*lpszName*包含一个有效的转换器的名称，选择它。 否则为\<否转换器 > 处于选中状态。  
  
 如果用户选择\<否转换器 > 的内容*lpszName*， *lpszPath*，并且*pvOption*不接触。 **SQLGetTranslator**设置*pcbNameOut*并*pcbPathOut*为 0，则返回 TRUE。  
  
 如果用户选择转换器**SQLGetTranslator**调用**ConfigTranslator**翻译人员的安装程序 DLL 中。 如果**ConfigTranslator**将返回 FALSE， **SQLGetTranslator**返回到其对话框。 如果**ConfigTranslator** ，则返回 TRUE， **SQLGetTranslator**返回 TRUE，以及所选的翻译名称、 路径和转换选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|配置转换器|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|获取转换属性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|设置转换属性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
