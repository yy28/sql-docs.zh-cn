---
title: SQLConfigDataSource 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ef74d98102c424a71ac1728d664fddbeac2296c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258858"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource Function
**符合性**  
 版本引入了：ODBC 1.0  
  
 **摘要**  
 **SQLConfigDataSource**添加、 修改或删除数据源。  
  
 功能**SQLConfigDataSource**还可以访问与[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>参数  
 *hwndParent*  
 [输入]父窗口句柄。 如果句柄为空，该函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_ADD_DSN:添加新的用户数据源。  
  
 ODBC_CONFIG_DSN:配置 （修改） 的现有用户数据源。  
  
 ODBC_REMOVE_DSN:删除现有用户数据源。  
  
 ODBC_ADD_SYS_DSN:添加新的系统数据源。  
  
 ODBC_CONFIG_SYS_DSN:修改现有的系统数据源。  
  
 ODBC_REMOVE_SYS_DSN:删除现有的系统数据源。  
  
 ODBC_REMOVE_DEFAULT_DSN:从系统信息删除默认数据源规范部分。 （它还会删除默认驱动程序规范部分中的系统信息的 Odbcinst.ini 条目。 这*fRequest*执行相同的功能已弃用**SQLRemoveDefaultDataSource**函数。)当指定此选项时，所有其他参数在调用**SQLConfigDataSource**应为 null 值; 如果它们不为空，将忽略它们。  
  
 *lpszDriver*  
 [输入]驱动程序说明 （通常关联 DBMS 的名称） 提供给用户而不是物理驱动器的名称。  
  
 *lpszAttributes*  
 [输入]双向以 null 结尾的关键字 / 值对的窗体中的属性列表。 有关详细信息，请参阅[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。 如果没有条目中的系统信息调用此函数时，该函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConfigDataSource**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*参数为无效或为 NULL。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*参数不是以下之一：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*参数无效。 它找不到注册表中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字值对|*LpszAttributes*参数包含语法错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|安装程序无法执行请求的操作*fRequest*参数。 在调用**ConfigDSN**失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装程序库|无法加载驱动程序安装程序库。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLConfigDataSource**使用的值*lpszDriver*要读取的系统信息中的驱动程序安装程序 DLL 的完整路径。 它加载 DLL 并调用**ConfigDSN**使用的传递给它的参数。  
  
 **SQLConfigDataSource**是否找不到或加载安装程序 DLL，或者如果用户取消了对话框中，则返回 FALSE。 否则，它将返回其从收到的状态**ConfigDSN**。  
  
 **SQLConfigDataSource**映射系统 DSN *fRequest*向用户 DSN *fRequest*s (为 ODBC_ADD_DSN ODBC_ADD_SYS_DSN、 ODBC_CONFIG_DSN，和 ODBC_REMOVE_SYS_ ODBC_CONFIG_SYS_DSN到 ODBC_REMOVE_DSN DSN)。 为了区分用户和系统 Dsn **SQLConfigDataSource**设置根据下表配置模式的安装程序。 在返回前, **SQLConfigDataSource**将配置模式下重置为 BOTHDSN。 **ConfigDSN** （由驱动程序） 应调用**SQLWriteDSNToIni**并**SQLWritePrivateProfileString**来支持系统 DSN。 有关详细信息，请参阅[ConfigDSN 函数](../../../odbc/reference/syntax/configdsn-function.md)。  
  
|*fRequest*|配置模式|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除数据源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安装程序 DLL）|  
|从系统信息中删除数据源名称|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|将数据源名称添加到系统信息|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
