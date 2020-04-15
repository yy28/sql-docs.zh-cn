---
title: SQL安装翻译器Ex功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cf52c26bf9e4a26f13a27a0e763fbaa30bd18ec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302088"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLInstall 翻译器Ex**将有关转换器的信息添加到系统信息的 Odbcinst.ini 部分（HKEY_LOCAL_MACHINE_SOFTWARE_ODBC_ODBCINST。INI_ODBC 译员注册表项）。  
  
 **SQLInstall 翻译器Ex**的功能也可以与[ODBCCONF 一起访问。EXE](../../../odbc/odbcconf-exe.md).  
  
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
 *lpsz 翻译*  
 [输入]这必须包含描述转换器的关键字值对的双空终止列表。 有关关键字-值对语法的详细信息，请参阅[翻译器规范子键](../../../odbc/reference/install/translator-specification-subkeys.md)。  
  
 **翻译**器和**安装程序**关键字必须包含在*lpsz 转换器*字符串中。 翻译 DLL 随**翻译者**关键字一起列出，翻译器设置 DLL 随 **"设置"** 关键字一起列出。 每个对都用 NULL 字节终止，整个列表用 NULL 字节终止。 （即，两个 NULL 字节标记列表的末尾。*lpsz 转换器*的格式如下：  
  
 {0 转换器=*翻译-DLL 文件名*{0}*设置-DLL 文件名*{0}{0}0}0  
  
 *lpszPathin*  
 [输入]转换器要安装位置的完整路径或空指针。 如果*lpszPath*是空指针，则转换器将安装在系统目录中。  
  
 *lpszPathOut*  
 [输出]应安装转换器的目标目录的路径。 如果从未安装转换器，*则 lpszPathOut*与*lpszPathIn*相同。 如果之前安装译员，*则 lpszPathOut*是先前安装的路径。  
  
 *cbPathOutMax*  
 [输入]*lpszPathOut 的长度。*  
  
 *多巴帕路*  
 [输出]可在*lpszPathOut*中返回的字节总数。 如果可用于返回的字节数大于或等于*cbPathOutMax，**则 lpszPathOut*中的输出路径将截断为*pcbPathOutMax*减去空终止字符。 *pcbPathOut*参数可以是空指针。  
  
 *f请求*  
 [输入]请求的类型。 *fRequest*必须包含以下值之一：  
  
 ODBC_INSTALL_INQUIRY：询问可在哪里安装译员。  
  
 ODBC_INSTALL_COMPLETE：完成安装请求。  
  
 *lpdwUsageCount*  
 [输出]调用此函数后转换器的使用计数。  
  
 应用程序不应设置使用计数。 ODBC 将保留此计数。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstall 翻译器Ex**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*lpszPathOut*参数不够大，无法包含输出路径。 缓冲区包含截断路径。<br /><br /> *cbPathOutMax*参数为*0，fRequest*参数为ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*fRequest*参数不是以下参数之一：<br /><br /> ODBC_INSTALL_INQUIRYODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效关键字-值对|*lpsz 转换器*参数包含语法错误。|  
|ODBC_ERROR_INVALID_PATH|无效安装路径|*lpszPathIn*参数包含一个无效的路径。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效参数序列|*lpsz 转换器*参数不包含关键字-值对的列表。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法增加或递减注册表的组件使用量计数|安装程序未能增加转换器的使用计数。|  
  
## <a name="comments"></a>注释  
 **SQLInstall 翻译器Ex**提供了一种仅安装转换器的机制。 此函数实际上不会复制任何文件。 调用程序负责复制翻译文件。  
  
 **SQLInstall 转换器Ex**将已安装的转换器的组件使用量计数增加 1。 如果已存在转换器的版本，但译员的组件使用计数不存在，则新组件使用计数值设置为 2。  
  
 应用程序安装程序负责物理复制转换器文件和维护文件使用情况计数。 如果以前未安装转换器文件，应用程序安装程序必须复制文件或文件并创建文件或文件使用情况计数。 如果以前已安装该文件，安装程序只会增加文件使用情况计数。  
  
 如果应用程序以前安装了旧版本的转换器，则应卸载译员，然后重新安装，以便译员组件使用计数有效。 应调用**SQLRemove 转换器**来递减组件使用计数，然后调用**SQLInstall 翻译Ex**以增加组件使用计数。 应用程序安装程序必须用新文件替换旧文件或文件。 文件使用情况计数将保持不变，使用旧版本文件的其他应用程序现在将使用较新版本。  
  
 **SQLInstallTranslatorEx**中的*lpszPathOut*中的路径长度允许两阶段安装过程，因此应用程序可以通过使用 ODBC_INSTALL_INQUIRY 模式的*fRequest*调用**SQLInstallTranslatorEx**来确定应该是什么*cbPathOutMax。* 这将返回*pcbPathOut*缓冲区中可用的字节总数。 然后，可以使用 ODBC_INSTALL_COMPLETE *fRequest*和*cbPathOutMax*参数调用**sqlInstallTranslatorEx，** 该参数设置为*pcbPathOut*缓冲区中的值，以及 null 终止字符。  
  
 如果选择不将双相模型用于**SQLInstallTranslatorEx，** 则必须设置*cbPathOutMax*，该模型将目标目录路径的存储大小定义为 stdlib.h 中定义的值_MAX_PATH，以防止截断。  
  
 当*frequest* ODBC_INSTALL_COMPLETE时 **，SQLInstall 翻译Ex**不允许*lpszPathOut*为 NULL（或*cbPathOutMax*为 0）。 如果*fRequest*是ODBC_INSTALL_COMPLETE，则当可返回的字节数大于或等于*cbPathOutMax*时返回 FALSE，结果会出现截断。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回默认翻译选项|[配置转换器](../../../odbc/reference/syntax/configtranslator-function.md)|  
|选择译员|[SQLGet 转换器](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|删除译员|[SQL 删除转换器](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
