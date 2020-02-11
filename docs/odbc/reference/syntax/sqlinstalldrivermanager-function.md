---
title: SQLInstallDriverManager 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f1e3ac7f0a76c607fa07d6eb92d069d99ef5e0a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076214"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函数
**度**  
 引入的版本： ODBC 1.0： Windows XP Service Pack 2、Windows Server 2003 Service Pack 1 和更高版本的操作系统中不推荐使用  
  
 **总结**  
 **SQLInstallDriverManager**返回用于安装 ODBC core 组件的目标目录的路径。 调用程序必须实际将驱动程序管理器的文件复制到目标目录。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszPath*  
 输出安装的目标目录的路径。  
  
 *cbPathMax*  
 送*LpszPath*的长度。 它必须至少为 _MAX_PATH 字节。  
  
 *pcbPathOut*  
 输出在*lpszPath*中返回的总字节数（不包括 null 终止字节数）。 如果可返回的字节数大于或等于*cbPathMax*，则*lpszPath*中的路径将截断为*cbPathMax*减 null 终止字符。 *PcbPathOut*参数可以为 null 指针。  
  
## <a name="returns"></a>返回  
 如果此函数成功，则返回 TRUE，否则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverManager**返回 FALSE 时，可以* \** 通过调用**SQLInstallerError**获取关联的 pfErrorCode 值。 下表列出了可由**SQLInstallerError**返回的* \*pfErrorCode*值，并说明了此函数的上下文中的每个值。  
  
|*\*pfErrorCode*|错误|说明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出现错误，但没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|缓冲区长度无效|*LpszPath*参数不够大，无法包含输出路径。 缓冲区包含截断的路径。<br /><br /> *CbPathMax*参数小于 _MAX_PATH。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减组件使用率计数|安装程序未能递增 ODBC core 组件的使用计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行此功能。|  
  
## <a name="comments"></a>注释  
 调用**SQLInstallDriverManager**来返回 ODBC core 组件的路径，并递增系统信息中的组件使用计数。 如果驱动程序管理器的某个版本已存在，但该驱动程序的组件使用计数不存在，则新的 "组件使用计数" 值将设置为2。  
  
 应用程序安装程序负责物理复制核心组件文件并维护文件使用计数。 如果以前未安装核心组件文件，则应用程序安装程序必须复制文件，并创建文件使用计数。 如果以前安装过该文件，则安装程序只会递增文件使用计数。  
  
 如果应用程序安装程序以前安装了旧版本的驱动程序管理器，则应该卸载并重新安装核心组件，以便核心组件使用计数有效。 应该首先调用**SQLRemoveDriverManager**以减少组件使用计数。 然后，应调用**SQLInstallDriverManager**来递增组件使用计数。 应用程序安装程序必须用新文件替换旧的核心组件文件。 文件使用计数将保持不变，并且使用较旧版本核心组件文件的其他应用程序现在将使用较新版本的文件。  
  
 在全新安装 ODBC core 组件、驱动程序和转换器时，应用程序安装程序应按以下顺序调用以下函数： **SQLInstallDriverManager**、 **SQLInstallDriverEx**、 **SQLConfigDriver** （ *FRequest*为 ODBC_INSTALL_DRIVER），然后是**SQLInstallTranslatorEx**。 在卸载核心组件、驱动程序和转换器时，应用程序安装程序应按顺序调用以下函数： **SQLRemoveTranslator**、 **SQLRemoveDriver**和**SQLRemoveDriverManager**。 必须按此顺序调用这些函数。 在所有组件的升级中，所有卸载函数都应按顺序调用，然后应按顺序调用所有安装函数。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|请参阅|  
|---------------------------|---------|  
|添加、修改或删除驱动程序|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安装驱动程序|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安装转换器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|删除驱动程序|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|删除驱动程序管理器|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|删除转换器|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
