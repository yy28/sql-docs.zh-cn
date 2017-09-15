---
title: "ConfigDriver 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 037d4ffcbe7d81c6e4a9c1a524f5f4977621f277
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="configdriver-function"></a>ConfigDriver 函数
**一致性**  
 版本引入了： ODBC 2.5  
  
 **摘要**  
 **ConfigDriver**允许安装程序来执行安装和卸载函数而无需此程序以调用**ConfigDSN**。 此函数将执行特定于驱动程序的功能，例如创建特定于驱动程序的系统信息和在安装期间，执行 DSN 转换，以及在卸载过程清理系统信息修改。 此函数被公开的驱动程序安装程序 DLL 或单独的安装程序 DLL。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 *hwndParent*  
 [输入]父窗口句柄。 如果句柄为 null，函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_INSTALL_DRIVER： 安装新的驱动程序。  
  
 ODBC_REMOVE_DRIVER： 删除驱动程序。  
  
 此选项也可以是特定于驱动程序，在这种情况下*fRequest*的第一个选项的自变量必须从 ODBC_CONFIG_DRIVER_MAX + 1 开始。 *FRequest*任何其他选项的参数也必须从大于 ODBC_CONFIG_DRIVER_MAX + 1 的值启动。  
  
 *lpszDriver*  
 [输入]注册的系统信息的 Odbcinst.ini 键在驱动程序的名称。  
  
 *lpszArgs*  
 [输入]以 null 结尾的字符串，包含特定于驱动程序的自变量*fRequest*。  
  
 *lpszMsg*  
 [输出]以 null 结尾的字符串，包含来自驱动程序安装程序的输出消息。  
  
 *cbMsgMax*  
 [输入]长度*lpszMsg*。  
  
 *pcbMsgOut*  
 [输出]可用于在中返回的字节总数*lpszMsg*。  
  
 可用于返回的字节数是否大于或等于*cbMsgMax*中的输出消息*lpszMsg*截断为*cbMsgMax*减 null 终止字符。 *PcbMsgOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigDriver**返回 FALSE，一个关联* \*pfErrorCode*值发布到安装程序错误缓冲区调用**SQLPostInstallerError**可以通过调用获取和**SQLInstallerError**。 下表列出* \*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*自变量无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*自变量不是以下之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 小于或等于 ODBC_CONFIG_DRIVER_MAX 特定于驱动程序的选项。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*自变量无效。 它找不到注册表中。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|无法执行请求的操作*fRequest*自变量。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定于驱动程序或转换器错误|没有任何定义的 ODBC 安装程序错误特定于驱动程序的错误。 *SzError*对的调用中的自变量**SQLPostInstallerError**函数应包含特定于驱动程序的错误消息。|  
  
## <a name="comments"></a>注释  
  
### <a name="driver-specific-options"></a>特定于驱动程序选项  
 应用程序可以请求通过使用公开由驱动程序的特定于驱动程序的功能*fRequest*自变量。 *FRequest* ODBC_CONFIG_DRIVER_MAX 加 1，将为第一个选项，并且将从该值 1 递增其他选项。 应以 null 结尾的字符串中提供该函数由驱动程序所需的任何自变量传递中*lpszArgs*自变量。 提供此类功能的驱动程序应保持特定于驱动程序选项的表。 选项应完全记录在驱动程序文档。 使用特定于驱动程序选项的应用程序编写器应注意，这将使应用程序不太可互操作。  
  
### <a name="messages"></a>消息  
 驱动程序安装程序例程可以发送短信，向应用程序中以 null 结尾的字符串*lpszMsg*缓冲区。 消息将被截断为*cbMsgMax*通过的 null 终止字符减去**ConfigDriver**函数是否大于或等于*cbMsgMax*字符。
