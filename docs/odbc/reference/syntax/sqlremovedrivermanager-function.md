---
title: SQLRemoveDriverManager 函数 |Microsoft 文档
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
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad7508ef6825bda50adee02fe92665e4d3445ee5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918422"
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager 函数
**一致性**  
 版本引入： ODBC 3.0： 在 Windows XP Service Pack 2、 Windows Server 2003 Service Pack 1 和更高版本操作系统中已过时。  
  
 **摘要**  
 **SQLRemoveDriverManager**更改或删除中的系统信息的 Odbcinst.ini 条目有关 ODBC 核心组件的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *pdwUsageCount*  
 [输出]使用情况计数的驱动程序管理器后调用此函数中。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。 如果没有条目存在的系统信息中，调用此函数时，此函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDriverManager**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序无法删除驱动程序管理器信息，因为它在注册表中不存在或无法在注册表中找到。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法减少的使用情况计数的驱动程序管理器。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDriverManager**进行了补充**SQLInstallDriverManager**函数，并且更新的组件使用情况计数的系统信息。 只能从安装程序应用程序，应调用此函数。  
  
 **SQLRemoveDriverManager**将按 1 递减的核心组件使用计数。 如果组件使用情况计数归为 0，则将删除的条目系统信息。 核心组件条目已在"ODBC 核心"的标题下的系统信息中的以下位置：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  应用程序不应以物理方式删除驱动程序管理器文件的组件使用计数和文件使用情况计数达到零时。  
  
 **SQLRemoveDriverManager**不会实际删除任何文件。 调用程序负责删除文件和维护的文件使用情况计数。 驱动程序管理器文件应不是，但是，删除时的组件使用计数和文件使用率计数已达到零，因为这些文件可能由其他应用程序具有不会增加文件使用率计数。  
  
 **SQLRemoveDriverManager**作为卸载过程中调用。 作为一个整体卸载 ODBC 核心组件 （包括驱动程序管理器、 光标库，安装程序、 的语言库、 管理员、 形式转换文件和等等）。 以下文件不是删除时**SQLRemoveDriverManager**作为卸载过程中调用：  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32。DLL|  
|ODBCCR32。DLL|ODBC16GT。DLL|  
|ODBCCU32。DLL|ODBC32GT。DLL|  
|ODBCINT。DLL|DS16GT。DLL|  
|ODBCTRAC。DLL|DS32GT。DLL|  
|MSVCRT40。DLL|ODBCAD32。EXE|  
|ODBCCP32。CPL||  
  
 **SQLRemoveDriverManager**也称为升级过程的一部分。 如果应用程序检测到它已执行升级，以及它以前已安装该驱动程序，则应删除该驱动程序，并将其然后重新安装。  
  
 **SQLRemoveDriverManager**首先应调用以减少的组件使用情况计数。 **SQLInstallDriverEx**然后应调用以递增的组件使用计数。 应用程序安装程序必须用新的文件替换旧的核心组件文件。 文件使用情况计数将保持不变，并使用以前版本的核心组件文件的其他应用程序现在将使用较新版本文件。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|安装驱动程序管理器|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
