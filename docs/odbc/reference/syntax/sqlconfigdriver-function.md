---
title: SQL 配置驱动程序功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0da15cef06e5d8392408108ce88b53f7885eb65e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301242"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函数
**一致性**  
 版本介绍： ODBC 2.5  
  
 **摘要**  
 **SQLConfigDriver**加载相应的驱动程序设置 DLL 并调用**ConfigDriver**函数。  
  
 **SQLConfigDriver**的功能也可以与[ODBCCONF 一起访问。EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd 家长*  
 [输入]父窗口句柄。 如果句柄为空，则函数将不会显示任何对话框。  
  
 *f请求*  
 [输入]请求的类型。 *fRequest*必须包含以下值之一：  
  
 ODBC_CONFIG_DRIVER：更改驱动程序使用的连接池超时。  
  
 ODBC_INSTALL_DRIVER：安装新驱动程序。  
  
 ODBC_REMOVE_DRIVER：删除现有驱动程序。  
  
 此选项也可以特定于驱动程序，在这种情况下，第一个选项的*fRequest*必须从 ODBC_CONFIG_DRIVER_MAX+1 开始。 任何附加选项的*fRequest*也必须从大于 ODBC_CONFIG_DRIVER_MAX+1 的值开始。  
  
 *lpszDriver*  
 [输入]在系统信息中注册的驱动程序的名称。  
  
 *lpszArgs*  
 [输入]包含特定于驱动程序*的 fRequest*的参数的 null 端接字符串。  
  
 *lpszMsg*  
 [输出]包含驱动程序设置输出消息的 null 终止字符串。  
  
 *cbMsgMax*  
 [输入]*lpszMsg*的长度。  
  
 *巴布姆斯格*  
 [输出]可用以*lpszMsg*返回的字节总数。 如果可用于返回的字节数大于或等于*cbMsgMax，**则 lpszMsg*中的输出消息将被截断为*cbMsgMax*减去 null 终止字符。 *pcbMsgOut*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConfigDriver**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*lpszMsg*参数无效。|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd 父参数*无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*fRequest*参数不是以下参数之一：<br /><br /> ODBC_INSTALL_DRIVERODBC_REMOVE_DRIVER<br /><br /> *fRequest*参数是一个驱动程序特定的选项，小于或等于ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszDriver*参数无效。 在注册表中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效关键字-值对|*lpszArgs*参数包含语法错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|安装程序无法执行*fRequest*参数请求的操作。 对**ConfigDriver 的**调用失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器设置库|无法加载驱动程序设置库。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLConfigDriver**允许应用程序调用驱动程序的**ConfigDriver**例程，而无需知道名称并加载特定于驱动程序的安装程序 DLL。 安装驱动程序设置 DLL 后，安装程序调用此功能。 调用程序应注意，此函数可能并非对所有驱动程序都可用。 在这种情况下，调用程序应继续，没有错误。  
  
## <a name="driver-specific-options"></a>特定于驱动程序的选项  
 应用程序可以使用*fRequest*参数请求驱动程序公开的特定于驱动程序的功能。 第一个选项的*fRequest*将在ODBC_CONFIG_DRIVER_MAX+1，其他选项将从该值增加 1。 驱动程序为该函数所需的任何参数都应在*lpszArgs*参数中传递的 null 端接字符串中提供。 提供此类功能的驱动程序应维护特定于驱动程序的选项表。 选项应完整地记录在驱动程序文档中。 使用特定于驱动程序的选项的应用程序编写器应注意，此使用将使应用程序的互操作性降低。  
  
## <a name="setting-connection-pooling-timeout"></a>设置连接池超时  
 设置驱动程序的配置时，可以设置连接池超时属性。 **SQLConfigDriver**调用时，ODBC_CONFIG_DRIVER和*lpszArgs*的*frequest*设置为**CPTimeout。** **CPTimeout**确定连接可以在连接池中保留而不使用的时间周期。 超时过期时，连接将关闭并从池中删除。 默认超时为 60 秒。  
  
 当**SQLConfigDriver**调用*fRequest*设置为ODBC_INSTALL_DRIVER或ODBC_REMOVE_DRIVER时，驱动程序管理器将加载相应的驱动程序设置 DLL 并调用**ConfigDriver**函数。 当使用*fODBC_CONFIG_DRIVER调用* **SQLConfigDriver**时，所有处理都将在 ODBC 安装程序中执行，因此不必加载驱动程序设置 DLL。  
  
## <a name="messages"></a>消息  
 驱动程序设置例程可以将文本消息作为*lpszMsg*缓冲区中的 null 终止字符串发送到应用程序。 如果消息大于或等于*cbMsgMax*字符，则**ConfigDriver**函数将消息截断为*cbMsgMax*减去 null 终止字符。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除驱动程序|[配置驱动程序](../../../odbc/reference/syntax/configdriver-function.md)（在设置 DLL 中）|  
|删除默认数据源|[SQL 删除默认数据源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
