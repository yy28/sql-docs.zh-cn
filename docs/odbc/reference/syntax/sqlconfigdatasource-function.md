---
title: SQLConfigData源函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90a51193a8f4edbb013527c4dde0625b75131583
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299627"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource Function
**一致性**  
 版本介绍： ODBC 1.0  
  
 **摘要**  
 **SQLConfigDataSource**添加、修改或删除数据源。  
  
 **SQLConfigDataSource**的功能也可以与[ODBCCONF 一起访问。EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd 家长*  
 [输入]父窗口句柄。 如果句柄为空，则函数将不会显示任何对话框。  
  
 *f请求*  
 [输入]请求的类型。 *fRequest*参数必须包含以下值之一：  
  
 ODBC_ADD_DSN：添加新的用户数据源。  
  
 ODBC_CONFIG_DSN：配置（修改）现有用户数据源。  
  
 ODBC_REMOVE_DSN：删除现有用户数据源。  
  
 ODBC_ADD_SYS_DSN：添加新的系统数据源。  
  
 ODBC_CONFIG_SYS_DSN：修改现有系统数据源。  
  
 ODBC_REMOVE_SYS_DSN：删除现有系统数据源。  
  
 ODBC_REMOVE_DEFAULT_DSN：从系统信息中删除默认数据源规范部分。 （它还从系统信息中的 Odbcinst.ini 条目中删除默认驱动程序规范部分。 此*fRequest*执行的功能与弃用的**SQLRemoveDefaultDataSource**函数相同。指定此选项后，对**SQLConfigDataSource**的调用中的所有其他参数应为 NUL;对 SQL 调用时，所有其他参数都应为 NUL。如果它们不是 NULL，则将被忽略。  
  
 *lpszDriver*  
 [输入]向用户而不是物理驱动程序名称显示的驱动程序描述（通常是关联的 DBMS 的名称）。  
  
 *lpsz属性*  
 [输入]以关键字-值对形式加倍终止的属性列表。 有关详细信息，请参阅[配置DSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。 如果在调用此函数时系统信息中不存在条目，则函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConfigDataSource**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd 父参数*无效或 NULL。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*fRequest*参数不是以下参数之一：<br /><br /> ODBC_ADD_DSNODBC_CONFIG_DSN ODBC_REMOVE_DSNODBC_ADD_SYS_DSNODBC_CONFIG_SYS_DSNODBC_REMOVE_SYS_DSNODBC_REMOVE_DEFAULT_DSNODBC_CONFIG_DSN|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszDriver*参数无效。 在注册表中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效关键字-值对|*lpszAttributes*参数包含语法错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|安装程序无法执行*fRequest*参数请求的操作。 对**ConfigDSN 的**调用失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器设置库|无法加载驱动程序设置库。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLConfigDataSource**使用*lpszDriver*的值从系统信息读取驱动程序的安装程序 DLL 的完整路径。 它加载 DLL 并调用**ConfigDSN，** 其参数与传递给它的相同参数相同。  
  
 **如果 SQLConfigDataSource**无法查找或加载安装程序 DLL 或用户取消对话框，则返回 FALSE。 否则，它将返回从**ConfigDSN**收到的状态。  
  
 **SQLConfigDataSource**将系统 DSN *fRequest*映射到用户 DSN *fRequests（ODBC_ADD_SYS_DSN*到ODBC_ADD_DSN，ODBC_CONFIG_SYS_DSN到ODBC_CONFIG_DSN，ODBC_REMOVE_SYS_DSN到ODBC_REMOVE_DSN）。 为了区分用户和系统**DSN，SQLConfigDataSource**根据下表设置安装程序配置模式。 在返回之前 **，SQLConfigDataSource**会将配置模式重置为 BOTHDSN。 **配置DSN（** 由驱动程序实现）应调用**SQLWriteDSNToini**和**SQLWritePrivateProfileString**来支持系统 DSN。 有关详细信息，请参阅[配置DSN函数](../../../odbc/reference/syntax/configdsn-function.md)。  
  
|*f请求*|配置模式|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除数据源|[配置DSN（](../../../odbc/reference/syntax/configdsn-function.md)在设置 DLL 中）|  
|从系统信息中删除数据源名称|[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|向系统信息添加数据源名称|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
