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
manager: craigg
ms.openlocfilehash: 1bd012fc4f3d1e55c27a585600bff7f85459d469
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844355"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函数
**符合性**  
 版本引入了： ODBC 1.0： 在 Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更高版本操作系统中已过时  
  
 **摘要**  
 **SQLInstallDriverManager**返回 ODBC 核心组件的安装的目标目录的路径。 实际上，调用程序必须将驱动程序管理器的文件复制到目标目录。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszPath*  
 [输出]安装目标目录的路径。  
  
 *cbPathMax*  
 [输入]长度*lpszPath*。 这必须至少为 _max_path(256 个字节。  
  
 *pcbPathOut*  
 [输出]总字节数 （不包括 null 终止字节） 中返回*lpszPath*。 可用来返回的字节数是否大于或等于*cbPathMax*，在路径*lpszPath*将被截断为*cbPathMax*减去 null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverManager**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效缓冲区长度|*LpszPath*参数不是足够大以包含输出路径。 在缓冲区中包含的被截断的路径。<br /><br /> *CbPathMax*参数为 _MAX_PATH 小于。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法递增 ODBC 核心组件使用情况计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLInstallDriverManager**调用要为 ODBC 核心组件和增量的组件使用情况计数的系统信息中返回的路径。 如果已有某个版本的驱动程序管理器，但该驱动程序的组件使用计数不存在，则会将新组件使用情况计数值设置为 2。  
  
 应用程序安装程序负责以物理方式将复制的核心组件文件和维护的文件使用情况计数。 如果以前尚未安装的核心组件文件，应用程序安装程序必须复制该文件，并创建文件使用情况计数。 如果文件先前已安装，安装程序将只是递增的文件使用情况计数。  
  
 如果应用程序安装程序之前安装的较旧版本的驱动程序管理器中，应卸载，然后重新安装，以便核心组件使用情况计数是有效的核心组件。 **SQLRemoveDriverManager**首先应调用要递减的组件使用计数。 **SQLInstallDriverManager**然后应调用来增加的组件使用情况计数。 应用程序安装程序必须将新文件替换为旧的核心组件文件。 文件使用情况计数将保持不变，并使用较旧版本的核心组件文件的其他应用程序现在将使用较新版本文件。  
  
 在 ODBC 核心组件、 驱动程序和翻译人员的全新安装，应用程序安装程序应在序列中调用以下函数： **SQLInstallDriverManager**， **SQLInstallDriverEx**， **SQLConfigDriver** (与*fRequest* ODBC_INSTALL_DRIVER 的)，然后**SQLInstallTranslatorEx**。 中的核心组件、 驱动程序和翻译人员卸载，应用程序安装程序应在序列中调用以下函数： **SQLRemoveTranslator**， **SQLRemoveDriver**，，然后**SQLRemoveDriverManager**。 这些函数的调用必须按此顺序。 在升级过程中的所有组件，应按顺序调用所有卸载函数，然后按顺序都调用安装的所有函数。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除驱动程序|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安装驱动程序|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安装一个转换器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|删除驱动程序|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|删除驱动程序管理器|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|删除翻译|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
