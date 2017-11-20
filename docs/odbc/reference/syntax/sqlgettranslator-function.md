---
title: "SQLGetTranslator 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76bc8c85e923c792e87c13c2ca7f490c7273d975
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函数
**一致性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **SQLGetTranslator**显示一个对话框，用户可以从中选择一个转换器。  
  
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
  
 *在 lpszName*  
 [输入/输出]转换器中的系统信息的名称。  
  
 *cbNameMax*  
 [输入]最大长度*lpszName*缓冲区。  
  
 *pcbNameOut*  
 [输入/输出]总字节数 （不包括 null 终止字节） 传递或返回在*lpszName*。 可用于返回的字节数是否大于或等于*cbNameMax*中的转换器名称*lpszName*截断为*cbNameMax*减null 终止字符。 *PcbNameOut*参数可以是 null 指针。  
  
 *lpszPath*  
 [输出]转换 DLL 的完整路径。  
  
 *cbPathMax*  
 [输入]最大长度*lpszPath*缓冲区。  
  
 *pcbPathOut*  
 [输出]总字节数 （不包括 null 终止字节） 中返回*lpszPath*。 可用于返回的字节数是否大于或等于*cbPathMax*中的转换 DLL 路径*lpszPath*截断为*cbPathMax*减null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
 *pvOption*  
 [输出] 32 位转换选项。  
  
## <a name="returns"></a>返回  
 如果成功，则 FALSE 如果它出现故障，或者用户取消对话框中，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetTranslator**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*CbNameMax*或*cbPathMax*自变量为小于或等于 0。|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*自变量为无效或为空。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszName*自变量无效。 它找不到注册表中。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装库|无法加载转换器库。|  
|ODBC_ERROR_INVALID_OPTION|无效的事务选项|*PvOption*参数包含无效值。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 如果*hwndParent*为 null 或如果*lpszName*， *lpszPath*，或*pvOption*是 null 指针， **SQLGetTranslator**方法将返回 FALSE。 否则，它将在以下对话框中显示已安装的转换器列表。  
  
 ![选择转换器对话框](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果*lpszName*包含一个有效的转换器名称，选择它。 否则为\<否转换器 > 选择。  
  
 如果用户选择\<否转换器 > 的内容*lpszName*， *lpszPath*，和*pvOption*不接触。 **SQLGetTranslator**设置*pcbNameOut*和*pcbPathOut* 0，并且返回 TRUE。  
  
 如果用户选择转换器， **SQLGetTranslator**调用**ConfigTranslator**转换器的安装程序 DLL 中。 如果**ConfigTranslator**方法将返回 FALSE， **SQLGetTranslator**返回到其对话框。 如果**ConfigTranslator** ，则返回 TRUE， **SQLGetTranslator**返回 TRUE，以及所选的转换器名称、 路径和转换选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|配置一个转换器|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|获取转换属性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|设置转换属性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|

