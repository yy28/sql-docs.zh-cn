---
title: SQLRemoveDriverManager 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3413cf3c0e316e25ad52cc35ba348cab1694ae4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537408"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函数
**符合性**  
 版本引入了：ODBC 3.0:在 Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更高版本操作系统中已过时。  
  
 **摘要**  
 **SQLRemoveDriverManager**更改或删除从 Odbcinst.ini 条目的系统信息中有关 ODBC 核心组件的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *pdwUsageCount*  
 [输出]使用情况计数的驱动程序管理器后调用此函数中。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。 如果没有条目中的系统信息调用此函数时，该函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDriverManager**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序无法删除驱动程序管理器的信息，因为它在注册表中不存在或找不到注册表中。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法减少使用情况计数的驱动程序管理器。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDriverManager**进行了补充**SQLInstallDriverManager**函数，并且更新的组件使用情况计数中的系统信息。 只能从安装程序应用程序应调用此函数。  
  
 **SQLRemoveDriverManager**将核心组件使用情况计数递减 1。 如果组件使用情况计数达到 0，则将删除条目系统信息。 核心组件条目中下标题"ODBC 核心"的系统信息中的以下位置为：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  应用程序不应以物理方式删除驱动程序管理器文件时的组件使用计数和文件使用情况计数归零。  
  
 **SQLRemoveDriverManager**不会实际删除任何文件。 调用程序负责删除文件和维护的文件使用情况计数。 驱动程序管理器文件但是不应、 时被删除的组件使用计数和文件使用率计数已达到零，因为这些文件可能由其他应用程序具有不会增加文件使用情况计数。  
  
 **SQLRemoveDriverManager**作为卸载过程的一部分调用。 作为一个整体卸载 ODBC 核心组件 （其中包括驱动程序管理器、 光标库、 安装程序、 语言库、 管理员、 形式转换文件和等等）。 以下文件不是删除何时**SQLRemoveDriverManager**称为卸载过程的一部分：  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32.DLL|  
|ODBCCR32.DLL|ODBC16GT.DLL|  
|ODBCCU32.DLL|ODBC32GT.DLL|  
|ODBCINT.DLL|DS16GT.DLL|  
|ODBCTRAC.DLL|DS32GT.DLL|  
|MSVCRT40.DLL|ODBCAD32.EXE|  
|ODBCCP32.CPL||  
  
 **SQLRemoveDriverManager**也称为升级过程的一部分。 如果应用程序检测到它必须执行升级和它以前已安装的驱动程序，应删除并再重新安装该驱动程序。  
  
 **SQLRemoveDriverManager**首先应调用要递减的组件使用计数。 **SQLInstallDriverEx**然后应调用来增加的组件使用情况计数。 应用程序安装程序必须将新文件替换为旧的核心组件文件。 文件使用情况计数将保持不变，并使用较旧版本的核心组件文件的其他应用程序现在将使用较新版本文件。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|安装驱动程序管理器|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
