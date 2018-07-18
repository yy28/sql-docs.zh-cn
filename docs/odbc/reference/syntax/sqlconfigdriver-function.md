---
title: SQLConfigDriver 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a5fc4ac9aebbabf0181d42ae9d026aa697e8b58
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32919612"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函数
**一致性**  
 版本引入了： ODBC 2.5  
  
 **摘要**  
 **SQLConfigDriver**加载的适当的驱动程序安装程序 DLL 和调用**ConfigDriver**函数。  
  
 功能**SQLConfigDriver**还可通过访问[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 [输入]父窗口句柄。 如果句柄为 null，函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *fRequest*必须包含以下值之一：  
  
 ODBC_CONFIG_DRIVER： 更改连接池超时由驱动程序。  
  
 ODBC_INSTALL_DRIVER： 安装新的驱动程序。  
  
 ODBC_REMOVE_DRIVER： 删除现有的驱动程序。  
  
 此选项也可以是特定于驱动程序，在这种情况下*fRequest*为第一个选项必须从 ODBC_CONFIG_DRIVER_MAX + 1 开始。 *FRequest*为任何其他选项也必须从大于 ODBC_CONFIG_DRIVER_MAX + 1 的值启动。  
  
 *lpszDriver*  
 [输入]驱动程序的系统信息中注册的名称。  
  
 *lpszArgs*  
 [输入]包含的特定于驱动程序的自变量的以 null 结尾的字符串*fRequest*。  
  
 *lpszMsg*  
 [输出]包含来自驱动程序安装程序的输出消息的以 null 结尾的字符串。  
  
 *cbMsgMax*  
 [输入]长度*lpszMsg。*  
  
 *pcbMsgOut*  
 [输出]可用于在中返回的字节总数*lpszMsg*。 可用于返回的字节数是否大于或等于*cbMsgMax*中的输出消息*lpszMsg*截断为*cbMsgMax*减 null 终止字符。 *PcbMsgOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConfigDriver**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*LpszMsg*自变量无效。|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*自变量无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*自变量不是以下之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *FRequest*自变量为小于或等于 ODBC_CONFIG_DRIVER_MAX 特定于驱动程序的选项。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*自变量无效。 它找不到注册表中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字 / 值对|*LpszArgs*参数包含语法错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|安装程序无法执行请求的操作*fRequest*自变量。 调用**ConfigDriver**失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装库|无法加载驱动程序安装程序库。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLConfigDriver**允许应用程序调用驾**ConfigDriver**例程而无需知道的名称和加载特定于驱动程序的安装程序 DLL。 安装程序已安装 DLL 驱动程序安装完成后调用此函数。 调用程序应注意，此函数可能不会用于所有驱动程序。 在这种情况下，调用程序应继续正常。  
  
## <a name="driver-specific-options"></a>特定于驱动程序选项  
 应用程序可以请求通过使用公开由驱动程序的特定于驱动程序的功能*fRequest*自变量。 *FRequest* ODBC_CONFIG_DRIVER_MAX + 1，将为第一个选项，并且将从该值 1 递增其他选项。 应以 null 结尾的字符串中提供该函数由驱动程序所需的任何自变量传递中*lpszArgs*自变量。 提供此类功能的驱动程序应保持特定于驱动程序选项的表。 选项应完全记录在驱动程序文档。 使用特定于驱动程序选项的应用程序编写器应注意，此，请使用将使应用程序的较低的可互操作。  
  
## <a name="setting-connection-pooling-timeout"></a>设置连接池超时  
 设置驱动程序的配置时，可以设置连接池超时属性。 **SQLConfigDriver**使用调用*fRequest*的 ODBC_CONFIG_DRIVER 和*lpszArgs*设置为**CPTimeout**。 **CPTimeout**确定的连接可在不使用这样连接池中保留的时间段。 在超时到期，当连接关闭，并从池中删除。 默认超时为 60 秒。  
  
 当**SQLConfigDriver**使用调用*fRequest*设置为 ODBC_INSTALL_DRIVER 或 ODBC_REMOVE_DRIVER，驱动程序管理器加载的适当的驱动程序安装程序 DLL 和调用**ConfigDriver**函数。 当**SQLConfigDriver**使用调用*fRequest*的 ODBC_CONFIG_DRIVER，所有处理都执行在 ODBC 安装程序中，以便驱动程序安装程序 DLL 没有加载。  
  
## <a name="messages"></a>消息  
 驱动程序安装程序例程可以发送短信，向应用程序中以 null 结尾的字符串*lpszMsg*缓冲区。 消息将被截断为*cbMsgMax*通过的 null 终止字符减去**ConfigDriver**函数是否大于或等于*cbMsgMax*字符。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除驱动程序|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)（在安装程序 DLL）|  
|删除默认数据源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
