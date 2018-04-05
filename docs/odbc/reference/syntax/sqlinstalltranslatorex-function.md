---
title: SQLInstallTranslatorEx 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 220d3e6b0cc62c2d3d238332975c32e9c38bc030
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLInstallTranslatorEx**将翻译人员有关信息添加到系统信息 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST Odbcinst.ini 节。INI\ODBC 转换器注册表项）。  
  
 功能**SQLInstallTranslatorEx**还可通过访问[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpszTranslator*  
 [输入]这必须包含双向以 null 结尾的描述转换器的关键字 / 值对列表。 有关关键字 / 值对语法的详细信息，请参阅[转换器规范子项](../../../odbc/reference/install/translator-specification-subkeys.md)。  
  
 **转换器**和**安装**关键字必须包括在*lpszTranslator*字符串。 DLL 列在一起的转换**转换器**关键字，然后转换器安装程序 DLL 列出与**安装**关键字。 每个对终止与 NULL 字节，并且整个列表因 NULL 字节。 （也就是说，两个 NULL 字节标记列表的末尾。）格式*lpszTranslator*如下：  
  
 \0Translator=*转换器 DLL filename*\0[Setup=*安装程序 DLL filename*\0]\0  
  
 *lpszPathIn*  
 [输入]转换器其中是要安装或 null 指针的完整路径。 如果*lpszPath*是 null 指针，转换器将安装在系统目录。  
  
 *lpszPathOut*  
 [输出]应安装转换器的目标目录的路径。 如果永远不会安装了转换器， *lpszPathOut*相同*lpszPathIn*。 如果存在的转换器，先前安装*lpszPathOut*是先前安装的路径。  
  
 *cbPathOutMax*  
 [输入]长度*lpszPathOut。*  
  
 *pcbPathOut*  
 [输出]可用于在中返回的字节总数*lpszPathOut*。 可用于返回的字节数是否大于或等于*cbPathOutMax*中的输出路径*lpszPathOut*截断为*pcbPathOutMax*减null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
 *fRequest*  
 [输入]请求的类型。 *fRequest*必须包含以下值之一：  
  
 有关可以在其中安装转换器 Inquire ODBC_INSTALL_INQUIRY:。  
  
 ODBC_INSTALL_COMPLETE： 完成了安装请求。  
  
 *lpdwUsageCount*  
 [输出]转换器后调用此函数使用情况计数。  
  
 应用程序不应设置的使用计数。 ODBC 将维护此计数。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallTranslatorEx**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*LpszPathOut*自变量不为大到足以包含的输出路径。 在缓冲区中包含的截断的路径。<br /><br /> *CbPathOutMax*自变量为 0，和*fRequest*自变量为 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*自变量不是以下之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字 / 值对|*LpszTranslator*参数包含语法错误。|  
|ODBC_ERROR_INVALID_PATH|无效的安装路径|*LpszPathIn*参数包含无效的路径。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效的参数序列|*LpszTranslator*自变量不包含的关键字 / 值对的列表。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减注册表的组件使用率计数|安装程序无法递增转换器的使用情况计数。|  
  
## <a name="comments"></a>注释  
 **SQLInstallTranslatorEx**提供一种机制来安装仅转换器。 此函数实际上不复制任何文件。 调用程序负责将转换器文件复制。  
  
 **SQLInstallTranslatorEx**安装转换器的组件使用计数递增 1。 如果已经存在转换器的版本，但对该转换器的组件使用计数不存在，则将新组件使用情况计数值设置为 2。  
  
 应用程序安装程序负责以物理方式复制转换器文件和维护的文件使用计数。 如果该转换器文件以前尚未安装，应用程序安装程序必须复制或多个文件，并创建或多个文件使用率计数。 如果以前已安装文件，安装程序只需增加文件使用率计数。  
  
 如果较旧版本的转换器以前已安装应用程序，则应卸载转换器，并将其然后重新安装，以便转换器组件使用率计数无效。 **SQLRemoveTranslator**应调用以递减的组件使用计数，然后**SQLInstallTranslatorEx**应调用以递增的组件使用计数。 应用程序安装程序必须使用新的文件替换旧的文件。 文件使用情况计数将保持不变，并使用较旧版本文件的其他应用程序现在将使用较新版本。  
  
 中的路径的长度*lpszPathOut*中**SQLInstallTranslatorEx**允许对于的两阶段安装进程，因此应用程序可以确定什么*cbPathOutMax*应可通过调用**SQLInstallTranslatorEx**与*fRequest*的 ODBC_INSTALL_INQUIRY 模式。 这将返回中可用的字节总数*pcbPathOut*缓冲区。 **SQLInstallTranslatorEx**然后可以使用调用*fRequest*的 ODBC_INSTALL_COMPLETE 和*cbPathOutMax*参数设置中的值为*pcbPathOut*缓冲区，加上的 null 终止字符。  
  
 如果你选择不使用的两阶段模型**SQLInstallTranslatorEx**，必须设置*cbPathOutMax*，其定义为值 _MAX_PATH，到的目标目录的路径的存储大小定义在 Stdlib.h 中以防止发生截断。  
  
 当*fRequest*是 ODBC_INSTALL_COMPLETE， **SQLInstallTranslatorEx**不允许*lpszPathOut*为 NULL (或*cbPathOutMax*若要为 0）。 如果*fRequest* ODBC_INSTALL_COMPLETE，如果可用于返回的字节数大于或等于 FALSE 则返回*cbPathOutMax*，使用结果进行该截断。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回默认翻译选项|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|选择转换器|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|删除翻译|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
