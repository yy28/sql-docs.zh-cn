---
title: SQLConfigDriver 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e324b1f49bd6f8d0cad15ac2bcde73f558220330
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121449"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函数
**符合性**  
 版本引入了：ODBC 2.5  
  
 **摘要**  
 **SQLConfigDriver**加载相应的驱动程序安装程序 DLL 并调用**ConfigDriver**函数。  
  
 功能**SQLConfigDriver**还可以访问与[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
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
 *hwndParent*  
 [输入]父窗口句柄。 如果句柄为空，该函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *fRequest*必须包含以下值之一：  
  
 ODBC_CONFIG_DRIVER:更改连接池超时驱动程序使用。  
  
 ODBC_INSTALL_DRIVER:安装新的驱动程序。  
  
 ODBC_REMOVE_DRIVER:删除现有的驱动程序。  
  
 此选项也可以是特定于驱动程序，在这种情况下*fRequest*的第一个选项必须从 ODBC_CONFIG_DRIVER_MAX + 1 开始。 *FRequest*的任何其他选项也必须从大于 ODBC_CONFIG_DRIVER_MAX + 1 的值启动。  
  
 *lpszDriver*  
 [输入]在系统信息中注册的驱动程序的名称。  
  
 *lpszArgs*  
 [输入]以 null 结尾的字符串，其中包含驱动程序特定的参数*fRequest*。  
  
 *lpszMsg*  
 [输出]以 null 结尾的字符串，其中包含来自驱动程序安装程序的输出消息。  
  
 *cbMsgMax*  
 [输入]长度*lpszMsg。*  
  
 *pcbMsgOut*  
 [输出]可用于在返回的字节总数*lpszMsg*。 可用来返回的字节数是否大于或等于*cbMsgMax*中的输出消息*lpszMsg*将被截断为*cbMsgMax*减去 null 终止字符。 *PcbMsgOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConfigDriver**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|Error|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效缓冲区长度|*LpszMsg*参数无效。|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*参数无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*参数不是以下之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *FRequest*参数为小于或等于 ODBC_CONFIG_DRIVER_MAX 特定于驱动程序的选项。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*参数无效。 它找不到注册表中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字值对|*LpszArgs*参数包含语法错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|安装程序无法执行请求的操作*fRequest*参数。 在调用**ConfigDriver**失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装程序库|无法加载驱动程序安装程序库。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLConfigDriver**允许应用程序调用的驱动程序**ConfigDriver**例程而无需知道的名称和加载特定于驱动程序安装程序 DLL。 安装程序 DLL 已安装驱动程序安装完成后调用此函数。 调用程序应注意，此函数可能适用于所有驱动程序。 在这种情况下，调用程序应继续不会出错。  
  
## <a name="driver-specific-options"></a>特定于驱动程序的选项  
 应用程序可以请求通过使用公开的驱动程序的特定于驱动程序的功能*fRequest*参数。 *FRequest* ODBC_CONFIG_DRIVER_MAX + 1，将第一个选项，并将该值从 1 递增的其他选项。 所需驱动程序应以 null 结尾的字符串中提供该函数对任何自变量传入*lpszArgs*参数。 提供此类功能的驱动程序应维护特定于驱动程序的选项的表。 选项应完全记录在驱动程序文档。 应注意，这种用法将使应用程序的较低的可互操作应用程序编写器使用特定于驱动程序的选项。  
  
## <a name="setting-connection-pooling-timeout"></a>设置连接池超时  
 设置驱动程序的配置时，可以设置连接池超时属性。 **SQLConfigDriver**使用调用*fRequest*的 ODBC_CONFIG_DRIVER 和*lpszArgs*设置为**CPTimeout**。 **CPTimeout**确定的连接在连接池中可以保持而无需使用的时间段。 当超时到期时，连接关闭，并从池中删除。 默认超时为 60 秒。  
  
 当**SQLConfigDriver**使用调用*fRequest*设置为 ODBC_INSTALL_DRIVER 或 ODBC_REMOVE_DRIVER，驱动程序管理器将加载相应的驱动程序安装程序 DLL 并调用**ConfigDriver**函数。 当**SQLConfigDriver**使用调用*fRequest*的 ODBC_CONFIG_DRIVER，所有处理工作都都在 ODBC 安装程序中，以便不需要加载驱动程序安装程序 DLL。  
  
## <a name="messages"></a>消息  
 驱动程序安装例程可以将一条短信发送到应用程序中以 null 结尾的字符串作为*lpszMsg*缓冲区。 该消息将被截断为*cbMsgMax*减号的 null 终止字符**ConfigDriver**函数是否大于或等于*cbMsgMax*字符。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除驱动程序|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)（在安装程序 DLL）|  
|删除默认数据源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
