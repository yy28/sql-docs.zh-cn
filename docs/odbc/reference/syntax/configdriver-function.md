---
title: 配置驱动程序功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a2da5fd5ce01bd97f13d7c8d805c615c1ac436a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303958"
---
# <a name="configdriver-function"></a>ConfigDriver 函数
**一致性**  
 版本介绍： ODBC 2.5  
  
 **摘要**  
 **配置驱动程序**允许安装程序执行安装和卸载功能，而无需程序调用**ConfigDSN**。 此功能将执行特定于驱动程序的功能，例如创建特定于驱动程序的系统信息并在安装期间执行 DSN 转换，以及在卸载期间清理系统信息修改。 此功能由驱动程序设置 DLL 或单独的设置 DLL 公开。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd 家长*  
 [输入]父窗口句柄。 如果句柄为空，则函数将不会显示任何对话框。  
  
 *f请求*  
 [输入]请求的类型。 *fRequest*参数必须包含以下值之一：  
  
 ODBC_INSTALL_DRIVER：安装新驱动程序。  
  
 ODBC_REMOVE_DRIVER：删除驱动程序。  
  
 此选项也可以特定于驱动程序，在这种情况下，第一个选项的*fRequest*参数必须从 ODBC_CONFIG_DRIVER_MAX+1 开始。 任何附加选项的*fRequest*参数也必须从大于ODBC_CONFIG_DRIVER_MAX+1的值开始。  
  
 *lpszDriver*  
 [输入]在系统信息的 Odbcinst.ini 密钥中注册的驱动程序的名称。  
  
 *lpszArgs*  
 [输入]包含特定于驱动程序*的 fRequest*参数的 null 端接字符串。  
  
 *lpszMsg*  
 [输出]包含驱动程序设置输出消息的 null 端接字符串。  
  
 *cbMsgMax*  
 [输入]*lpszMsg*的长度 。  
  
 *巴布姆斯格*  
 [输出]可用以*lpszMsg*返回的字节总数。  
  
 如果可用于返回的字节数大于或等于*cbMsgMax，**则 lpszMsg*中的输出消息将被截断为*cbMsgMax*减去 null 终止字符。 *pcbMsgOut*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigDriver**返回 FALSE 时，通过调用**SQLPost 安装程序错误**将关联的*\*pfError 代码*值发布到安装程序错误缓冲区，并且可以通过调用**SQL 安装程序错误**获得。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd 父参数*无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*fRequest*参数不是以下参数之一：<br /><br /> ODBC_INSTALL_DRIVERODBC_REMOVE_DRIVER<br /><br /> 特定于驱动程序的选项小于或等于ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszDriver*参数无效。 在注册表中找不到它。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|无法执行*fRequest*参数请求的操作。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驱动程序或转换器特定错误|驱动程序特定的错误，没有定义的 ODBC 安装程序错误。 调用**SQLPost 安装程序错误**函数时 *，SzError*参数应包含特定于驱动程序的错误消息。|  
  
## <a name="comments"></a>注释  
  
### <a name="driver-specific-options"></a>特定于驱动程序的选项  
 应用程序可以使用*fRequest*参数请求驱动程序公开的特定于驱动程序的功能。 第一个选项的*fRequest*将ODBC_CONFIG_DRIVER_MAX加 1，其他选项将从该值增加 1。 驱动程序为该函数所需的任何参数都应在*lpszArgs*参数中传递的 null 端接字符串中提供。 提供此类功能的驱动程序应维护特定于驱动程序的选项表。 选项应完整地记录在驱动程序文档中。 使用特定于驱动程序的选项的应用程序编写器应注意，这将使应用程序的互操作性降低。  
  
### <a name="messages"></a>消息  
 驱动程序设置例程可以将文本消息作为*lpszMsg*缓冲区中的 null 终止字符串发送到应用程序。 如果消息大于或等于*cbMsgMax*字符，则**ConfigDriver**函数将消息截断为*cbMsgMax*减去 null 终止字符。
