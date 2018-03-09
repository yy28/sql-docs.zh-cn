---
title: "SQLInstallDriverManager 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallDriverManager
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallDriverManager
helpviewer_keywords: SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d1769b4951662f99cd50709b498891540fd4b9c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函数
**一致性**  
 版本引入： ODBC 1.0： 在 Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更高版本操作系统中已过时  
  
 **摘要**  
 **SQLInstallDriverManager**返回的 ODBC 核心组件安装的目标目录的路径。 实际上，调用程序必须将驱动程序管理器的文件复制到目标目录。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszPath*  
 [输出]安装的目标目录的路径。  
  
 *cbPathMax*  
 [输入]长度*lpszPath*。 这必须是至少 _MAX_PATH 字节。  
  
 *pcbPathOut*  
 [输出]总字节数 （不包括 null 终止字节） 中返回*lpszPath*。 可用于返回的字节数是否大于或等于*cbPathMax*中的路径*lpszPath*截断为*cbPathMax*减 null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverManager**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*LpszPath*自变量不为大到足以包含的输出路径。 在缓冲区中包含的截断的路径。<br /><br /> *CbPathMax*自变量为 _MAX_PATH 小于。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法递增 ODBC 核心组件使用率计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLInstallDriverManager**调用返回的路径，为 ODBC 核心组件和增量的组件使用情况计数的系统信息。 如果已经存在的版本的驱动程序管理器，但该驱动程序的组件使用计数不存在，则会将新组件使用情况计数值设置为 2。  
  
 应用程序安装程序负责以物理方式复制的核心组件文件和维护的文件使用情况计数。 如果以前尚未安装核心组件文件，应用程序安装程序必须复制该文件，并创建的文件使用计数。 如果以前已安装文件，安装程序将只是递增的文件使用情况计数。  
  
 如果旧版本的驱动程序管理器以前已安装的应用程序安装程序，则应卸载的核心组件，并将其然后重新安装，以便的核心组件使用计数无效。 **SQLRemoveDriverManager**首先应调用以减少的组件使用情况计数。 **SQLInstallDriverManager**然后应调用以递增的组件使用计数。 应用程序安装程序必须用新的文件替换旧的核心组件文件。 文件使用情况计数将保持不变，并使用以前版本的核心组件文件的其他应用程序现在将使用较新版本文件。  
  
 在 ODBC 核心组件、 驱动程序和翻译的全新安装，应用程序安装程序应按顺序调用以下函数： **SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLConfigDriver** (与*fRequest* ODBC_INSTALL_DRIVER 的)，然后**SQLInstallTranslatorEx**。 中的核心组件、 驱动程序和翻译卸载，应用程序安装程序应按顺序调用以下函数： **SQLRemoveTranslator**， **SQLRemoveDriver**，，然后**SQLRemoveDriverManager**。 必须在此序列中调用这些函数。 在升级过程中的所有组件，应按顺序调用所有卸载函数和安装的所有函数都应按顺序时都都调用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除驱动程序|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安装驱动程序|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安装一个转换器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|删除驱动程序|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|删除驱动程序管理器|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|删除翻译|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
