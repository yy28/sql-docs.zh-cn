---
title: SQL删除驱动程序管理器功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27b32c1c4e0f3f4d5359af287ba07d40b033af00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301808"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函数
**一致性**  
 介绍的版本：ODBC 3.0：在 Windows XP 服务包 2、Windows 服务器 2003 服务包 1 和更高版本的操作系统中弃用。  
  
 **摘要**  
 **SQLRemoveDriverManager**更改或删除系统信息中的 Odbcinst.ini 条目中有关 ODBC 核心组件的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *pdwUsageCount*  
 [输出]调用此函数后驱动程序管理器的使用计数。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。 如果在调用此函数时系统信息中不存在条目，则函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemove 驱动程序管理器**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|注册表中找不到组件|安装程序无法删除驱动程序管理器信息，因为它要么不存在在注册表中，要么在注册表中找不到。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法增加或递减组件使用量计数|安装程序未能减少驱动程序管理器的使用计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDriverManager**补充**SQLInstallDriverManager**功能，并更新系统信息中的组件使用情况计数。 应仅从设置应用程序调用此功能。  
  
 **SQLRemoveDriverManager**将核心组件使用计数减少 1。 如果组件使用计数为 0，则入口系统信息将被删除。 核心组件条目位于系统信息中的以下位置，标题为"ODBC 核心"：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  当组件使用计数和文件使用计数达到零时，应用程序不应物理删除驱动程序管理器文件。  
  
 **SQLRemove驱动程序管理器**实际上不会删除任何文件。 调用程序负责删除文件和维护文件使用情况计数。 但是，当组件使用计数和文件使用计数都达到零时，不应删除驱动程序管理器文件，因为这些文件可能由未增加文件使用计数的其他应用程序使用。  
  
 **SQLRemoveDriverManager**是作为卸载过程的一部分调用的。 ODBC 核心组件（包括驱动程序管理器、游标库、安装程序、语言库、管理员、文件等）作为一个整体卸载。 在作为卸载过程的一部分调用**SQLRemoveDriverManager**时，不会删除以下文件：  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32.Dll|  
|ODBCCR32.Dll|ODBC16GT.Dll|  
|ODBCCU32.Dll|ODBC32GT.Dll|  
|ODBCINT.Dll|DS16GT.Dll|  
|ODBCTRAC。Dll|DS32GT.Dll|  
|MSVCRT40。Dll|ODBCAD32.Exe|  
|ODBCCP32.Cpl||  
  
 **SQLRemoveDriverManager**也称为升级过程的一部分。 如果应用程序检测到必须执行升级，并且以前已安装驱动程序，则应删除驱动程序，然后重新安装驱动程序。  
  
 应首先调用**SQLRemoveDriverManager**来减少组件使用计数。 然后应调用**SQLInstallDriverEx**以增加组件使用计数。 应用程序安装程序必须用新文件替换旧的核心组件文件。 文件使用情况计数将保持不变，使用旧版本核心组件文件的其他应用程序现在将使用较新版本的文件。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|安装驱动程序管理器|[SQLInstall驱动程序管理器](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
