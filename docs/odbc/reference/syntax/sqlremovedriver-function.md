---
title: SQLRemoveDriver 函数 |Microsoft 文档
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
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77d92b7371c0ac262c9dcf6b4c57e8b9f1d7a26a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32919642"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLRemoveDriver**更改或删除中的系统信息的 Odbcinst.ini 条目有关驱动程序的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDriver*  
 [输入]注册的系统信息的 Odbcinst.ini 键在驱动程序的名称。  
  
 *fRemoveDSN*  
 [输入]有效值为：  
  
 TRUE： 删除与在指定的驱动程序相关联的 Dsn *lpszDriver*。 FALSE： 不删除与在指定的驱动程序相关联的 Dsn *lpszDriver*。  
  
 *lpdwUsageCount*  
 [输出]在调用此函数后的驱动程序使用情况计数。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。 如果没有条目存在的系统信息中，调用此函数时，此函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDriver**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序无法删除驱动程序信息，因为它在注册表中不存在或无法在注册表中找到。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*自变量无效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法减少该驱动程序的使用情况计数。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|*FRemoveDSN*参数为 TRUE; 但是，无法删除一个或多个 Dsn。 调用**SQLConfigDriver**与 ODBC_REMOVE_DRIVER 请求失败。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDriver**进行了补充[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)函数和更新的组件使用情况计数的系统信息。 只能从安装程序应用程序，应调用此函数。  
  
 **SQLRemoveDriver**将按 1 递减组件使用情况计数值。 如果组件使用率计数为 0，将执行以下操作：  
  
1.  **SQLConfigDriver**将调用函数使用 ODBC_REMOVE_DRIVER 选项。 如果*fRemoveDSN*选项设置为 TRUE， **ConfigDSN**函数调用**SQLRemoveDSNFromIni**删除与在指定的驱动程序相关联的所有数据源*lpszDriver。* 如果*fRemoveDSN*选项设置为 FALSE，将不会删除数据源。  
  
2.  将删除的系统信息中的驱动程序条目。 驱动程序条目已在以下的系统信息位置，在驱动程序名称下：  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**不会实际删除任何文件。 调用程序负责删除文件和维护的文件使用计数。 仅的组件使用计数和文件使用率计数已达到后零是以物理方式删除的文件。 可以删除组件中的某些文件，并且其他人不会删除，具体取决于是否将使用文件的其他应用程序具有递增文件使用率计数。  
  
 **SQLRemoveDriver**也称为升级过程的一部分。 如果应用程序检测到它已执行升级，以及它以前已安装该驱动程序，则应删除该驱动程序，并将其然后重新安装。 **SQLRemoveDriver**首先应调用以递减的组件使用计数，然后**SQLInstallDriverEx**应调用以递增的组件使用计数。 应用程序安装程序必须用新的文件替换旧的文件。 文件使用情况计数将保持不变，并使用以前版本的文件的其他应用程序现在将使用较新版本。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除驱动程序|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) （在安装程序 DLL）|  
|添加、 修改或删除驱动程序|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安装驱动程序|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
