---
title: ConfigDriver 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce34e46a49e88167606543a341aaef55591493ba
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538100"
---
# <a name="configdriver-function"></a>ConfigDriver 函数
**符合性**  
 版本引入了：ODBC 2.5  
  
 **摘要**  
 **ConfigDriver**允许执行安装和卸载函数而无需调用该程序的安装程序**ConfigDSN**。 此函数将执行特定于驱动程序的功能，如创建特定于驱动程序的系统信息和在安装期间，在执行 DSN 转换，以及在卸载过程中清理系统的信息修改。 此函数是由驱动程序安装程序 DLL 或单独的安装程序 DLL 公开的。  
  
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
 *hwndParent*  
 [输入]父窗口句柄。 如果句柄为空，该函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_INSTALL_DRIVER:安装新的驱动程序。  
  
 ODBC_REMOVE_DRIVER:删除驱动程序。  
  
 此选项也可以是特定于驱动程序，在这种情况下*fRequest*第一个选项的参数必须从 ODBC_CONFIG_DRIVER_MAX + 1 开始。 *FRequest*任何其他选项的参数也必须从大于 ODBC_CONFIG_DRIVER_MAX + 1 的值启动。  
  
 *lpszDriver*  
 [输入]在系统信息的 Odbcinst.ini 键中注册的驱动程序的名称。  
  
 *lpszArgs*  
 [输入]包含驱动程序特定的自变量的以 null 结尾的字符串*fRequest*。  
  
 *lpszMsg*  
 [输出]包含来自驱动程序安装程序的输出消息以 null 结尾的字符串。  
  
 *cbMsgMax*  
 [输入]长度*lpszMsg*。  
  
 *pcbMsgOut*  
 [输出]可用于在返回的字节总数*lpszMsg*。  
  
 可用来返回的字节数是否大于或等于*cbMsgMax*中的输出消息*lpszMsg*将被截断为*cbMsgMax*减去 null 终止字符。 *PcbMsgOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigDriver**返回 FALSE，关联 *\*pfErrorCode*值通过调用传递到安装程序错误缓冲区**SQLPostInstallerError**可以通过调用中获得**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*参数无效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*参数不是以下之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 特定于驱动程序的选项是小于或等于 ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*参数无效。 它找不到注册表中。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|无法执行请求的操作*fRequest*参数。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定于驱动程序或转换器错误|没有任何定义的 ODBC 安装程序错误特定于驱动程序的错误。 *SzError*调用中的参数**SQLPostInstallerError**函数应包含特定于驱动程序的错误消息。|  
  
## <a name="comments"></a>注释  
  
### <a name="driver-specific-options"></a>特定于驱动程序的选项  
 应用程序可以请求通过使用公开的驱动程序的特定于驱动程序的功能*fRequest*参数。 *FRequest* ODBC_CONFIG_DRIVER_MAX 加 1，将第一个选项，并将该值从 1 递增的其他选项。 所需驱动程序应以 null 结尾的字符串中提供该函数对任何自变量传入*lpszArgs*参数。 提供此类功能的驱动程序应维护特定于驱动程序的选项的表。 选项应完全记录在驱动程序文档。 应注意，这将使应用程序不到可互操作应用程序编写器使用特定于驱动程序的选项。  
  
### <a name="messages"></a>消息  
 驱动程序安装例程可以向作为以 null 结尾的字符串中的应用程序发送短信*lpszMsg*缓冲区。 该消息将被截断为*cbMsgMax*减号的 null 终止字符**ConfigDriver**函数是否大于或等于*cbMsgMax*字符。
