---
title: SQLInstallTranslatorEx 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57a2fb53226af9aeb6e546f6109a3e182ffc754f
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536558"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函数
**符合性**  
 版本引入了：ODBC 3.0  
  
 **摘要**  
 **SQLInstallTranslatorEx**将有关转换器的信息添加到 Odbcinst.ini 部分中的系统信息 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 翻译人员注册表项）。  
  
 功能**SQLInstallTranslatorEx**还可以访问与[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 [输入]这必须包含双向以 null 结尾的描述转换器的关键字值对的列表。 有关关键字值对语法的详细信息，请参阅[转换器规范子项](../../../odbc/reference/install/translator-specification-subkeys.md)。  
  
 **转换器**并**安装程序**关键字必须包含在*lpszTranslator*字符串。 DLL 列出与翻译**转换器**关键字和转换器安装程序 DLL 的下列出了带有**安装程序**关键字。 每个对终止 NULL 字节，并且整个列表终止 NULL 字节。 （也就是说，两个 NULL 字节标记列表的末尾。）格式*lpszTranslator*如下所示：  
  
 \0Translator=*translator-DLL-filename*\0[Setup=*setup-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [输入]转换器将在安装或 null 指针的完整路径。 如果*lpszPath*是 null 指针，转换器将安装在系统目录中。  
  
 *lpszPathOut*  
 [输出]翻译人员应安装的目标目录的路径。 如果转换器从未安装， *lpszPathOut*等同于*lpszPathIn*。 如果存在以前安装了转换器*lpszPathOut*是以前安装的路径。  
  
 *cbPathOutMax*  
 [输入]长度*lpszPathOut。*  
  
 *pcbPathOut*  
 [输出]可用于在返回的字节总数*lpszPathOut*。 可用来返回的字节数是否大于或等于*cbPathOutMax*中的输出路径*lpszPathOut*将被截断为*pcbPathOutMax*减null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
 *fRequest*  
 [输入]请求的类型。 *fRequest*必须包含以下值之一：  
  
 ODBC_INSTALL_INQUIRY:查询有关在其中安装转换器。  
  
 ODBC_INSTALL_COMPLETE:完成安装请求。  
  
 *lpdwUsageCount*  
 [输出]翻译后调用此函数的使用情况计数。  
  
 应用程序不应设置的使用计数。 ODBC 将保持此计数。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallTranslatorEx**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效缓冲区长度|*LpszPathOut*参数不是足够大以包含输出路径。 在缓冲区中包含的被截断的路径。<br /><br /> *CbPathOutMax*参数为 0，并且*fRequest*参数为 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*参数不是以下之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字值对|*LpszTranslator*参数包含语法错误。|  
|ODBC_ERROR_INVALID_PATH|无效的安装路径|*LpszPathIn*参数包含无效的路径。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效的参数序列|*LpszTranslator*参数不包含一系列关键字值对。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减注册表的组件使用情况计数|安装程序无法递增翻译人员的使用情况计数。|  
  
## <a name="comments"></a>注释  
 **SQLInstallTranslatorEx**提供了一种安装只需翻译的机制。 此函数不会实际复制的任何文件。 调用程序负责将翻译文件复制。  
  
 **SQLInstallTranslatorEx**已安装的转换器的组件使用计数递增 1。 如果已有某个版本的转换器，但不是存在对该转换器的组件使用计数，新组件使用情况计数值设置为 2。  
  
 应用程序安装程序是负责以物理方式将翻译文件的复制和维护文件使用情况计数。 如果转换器文件以前尚未安装，应用程序安装程序必须复制文件，并创建文件或文件使用率计数。 如果文件先前已安装，安装程序只需增加文件使用情况计数。  
  
 如果应用程序之前安装较旧版本的转换器，翻译人员应为卸载并再重新安装，以便有效的转换器组件使用计数。 **SQLRemoveTranslator**应调用要递减的组件使用计数，然后**SQLInstallTranslatorEx**应调用来增加的组件使用情况计数。 应用程序安装程序必须使用新文件替换旧的文件。 文件使用情况计数将保持不变，并使用较早的版本文件的其他应用程序现在将使用较新版本。  
  
 中的路径的长度*lpszPathOut*中**SQLInstallTranslatorEx**允许对两阶段的安装过程，因此应用程序可以确定什么*cbPathOutMax*应通过调用**SQLInstallTranslatorEx**与*fRequest* ODBC_INSTALL_INQUIRY 模式。 这将返回中可用的字节总数*pcbPathOut*缓冲区。 **SQLInstallTranslatorEx**然后可以使用调用*fRequest* ODBC_INSTALL_COMPLETE 的并且*cbPathOutMax*参数设置中的值为*pcbPathOut*缓冲区，再加上 null 终止字符。  
  
 如果您选择不使用的两阶段模型**SQLInstallTranslatorEx**，则必须设置*cbPathOutMax*，其定义的到值 _MAX_PATH 的目标目录的路径的存储大小为在 Stdlib.h 中定义，以防止发生截断。  
  
 当*fRequest*是 ODBC_INSTALL_COMPLETE， **SQLInstallTranslatorEx**不允许*lpszPathOut*为 NULL (或*cbPathOutMax*若要为 0）。 如果*fRequest* ODBC_INSTALL_COMPLETE，则返回 FALSE 时，将返回可用于返回的字节数是大于或等于*cbPathOutMax*，与结果发生截断。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回默认转换选项|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|选择转换器|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|删除翻译人员|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
