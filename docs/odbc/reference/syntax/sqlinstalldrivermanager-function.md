---
title: SQLInstall驱动程序管理器功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0788de0493439a360c0446733b31606a02e12422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302108"
---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager 函数
**一致性**  
 介绍的版本：ODBC 1.0：在 Windows XP 服务包 2、Windows 服务器 2003 服务包 1 和更高版本的操作系统中弃用  
  
 **摘要**  
 **SQLInstallDriverManager**返回用于安装 ODBC 核心组件的目标目录的路径。 调用程序必须实际将驱动程序管理器的文件复制到目标目录。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszPath*  
 [输出]安装的目标目录的路径。  
  
 *cbPathMax*  
 [输入]*lpszPath*的长度 。 这必须至少为_MAX_PATH字节。  
  
 *多巴帕路*  
 [输出]在*lpszPath*中返回的字节总数（不包括空终止字节）。 如果可用于返回的字节数大于或等于*cbPathMax，* 则*lpszPath*中的路径将被截断为*cbPathMax*减去空终止字符。 *pcbPathOut*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverManager**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*lpszPath*参数不够大，无法包含输出路径。 缓冲区包含截断路径。<br /><br /> *cbPathMax*参数小于_MAX_PATH。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法增加或递减组件使用量计数|安装程序未能增加 ODBC 核心组件使用量计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 调用**SQLInstallDriverManager**返回 ODBC 核心组件的路径，并增加系统信息中的组件使用计数。 如果驱动程序管理器的版本已存在，但驱动程序的组件使用计数不存在，则新的组件使用计数值设置为 2。  
  
 应用程序安装程序负责物理复制核心组件文件并维护文件使用情况计数。 如果以前未安装核心组件文件，应用程序安装程序必须复制该文件，并创建文件使用情况计数。 如果以前已安装该文件，安装程序只会增加文件使用情况计数。  
  
 如果应用程序安装程序以前安装了旧版本的驱动程序管理器，则应卸载核心组件，然后重新安装，以便核心组件使用计数有效。 应首先调用**SQLRemoveDriverManager**来减少组件使用计数。 然后应调用**SQLInstallDriverManager**以增加组件使用计数。 应用程序安装程序必须用新文件替换旧的核心组件文件。 文件使用情况计数将保持不变，使用旧版本核心组件文件的其他应用程序现在将使用较新版本的文件。  
  
 在重新安装 ODBC 核心组件、驱动程序和转换器时，应用程序安装程序应按顺序*fRequest*调用以下函数：SQLInstallDriverManager、SQLInstallDriverEx、SQLConfigDriver（带有 ODBC_INSTALL_DRIVER请求），然后是**SQLInstallDriverManager** **SQLInstall 翻译器Ex。** **SQLInstallDriverEx** **SQLConfigDriver** 在卸载核心组件、驱动程序和转换器时，应用程序安装程序应按顺序调用以下函数 **：SQLRemove 转换器****、SQLRemoveDriver，** 然后是**SQLRemoveDriverManager**。 这些函数必须按此顺序调用。 在升级所有组件时，应按顺序调用所有卸载功能，然后按顺序调用所有安装功能。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除驱动程序|[SQL 配置驱动程序](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安装驱动程序|[SQL安装驱动程序Ex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|安装翻译器|[SQL安装翻译器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|删除驱动程序|[SQL 删除驱动程序](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|删除驱动程序管理器|[SQL删除驱动程序管理器](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|删除转换器|[SQL 删除转换器](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
