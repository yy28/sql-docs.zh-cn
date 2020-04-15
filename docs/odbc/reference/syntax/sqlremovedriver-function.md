---
title: SQL删除驱动程序功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205c5b46e5f6cea195094f7a50e81d7509927d1a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303928"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLRemoveDriver**更改或删除系统信息中的 Odbcinst.ini 条目中有关驱动程序的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDriver*  
 [输入]在系统信息的 Odbcinst.ini 密钥中注册的驱动程序的名称。  
  
 *f 删除DSN*  
 [输入]有效值为：  
  
 TRUE：删除与*lpszDriver*中指定的驱动程序关联的 DSN。 FALSE：不要删除与*lpszDriver*中指定的驱动程序关联的 DSN。  
  
 *lpdwUsageCount*  
 [输出]调用此函数后驱动程序的使用计数。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。 如果在调用此函数时系统信息中不存在条目，则函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDriver**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|注册表中找不到组件|安装程序无法删除驱动程序信息，因为它要么不存在在注册表中，要么在注册表中找不到。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszDriver*参数无效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法增加或递减组件使用量计数|安装程序未能减少驱动程序的使用计数。|  
|ODBC_ERROR_REQUEST_FAILED|申请失败。|*fRemoveDSN*参数为 TRUE;但是，无法删除一个或多个 DSN。 对**SQLConfigDriver**的调用ODBC_REMOVE_DRIVER请求失败。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDriver**补充[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)功能，并更新系统信息中的组件使用情况计数。 应仅从设置应用程序调用此功能。  
  
 **SQLRemoveDriver**将组件使用计数值减少 1。 如果组件使用计数为 0，则会发生以下情况：  
  
1.  将调用带有ODBC_REMOVE_DRIVER选项的**SQLConfigDriver**函数。 如果*fRemoveDSN*选项设置为 TRUE，**则 ConfigDSN**函数将调用**SQLRemoveDSNFromIni**以删除与*lpszDriver*中指定的驱动程序关联的所有数据源。 如果*fRemoveDSN*选项设置为 FALSE，则不会删除数据源。  
  
2.  系统信息中的驱动程序条目将被删除。 驱动程序条目位于以下系统信息位置，在驱动程序名称下：  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**实际上不会删除任何文件。 调用程序负责删除文件和维护文件使用情况计数。 只有在组件使用计数和文件使用计数都达到零后，才会物理删除文件。 组件中的某些文件可以删除，而其他文件不会删除，具体取决于其他应用程序是否使用文件，这些应用程序增加了文件使用量计数。  
  
 **SQLRemoveDriver**也称为升级过程的一部分。 如果应用程序检测到必须执行升级，并且以前已安装驱动程序，则应删除驱动程序，然后重新安装驱动程序。 应首先调用**SQLRemoveDriver**来递减组件使用计数，然后调用**SQLInstallDriverEx**以增加组件使用计数。 应用程序安装程序必须用新文件替换旧文件。 文件使用情况计数将保持不变，使用旧版本文件的其他应用程序现在将使用较新版本。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除驱动程序|[配置驱动程序](../../../odbc/reference/syntax/configdriver-function.md)（在设置 DLL 中）|  
|添加、修改或删除驱动程序|[SQL 配置驱动程序](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安装驱动程序|[SQL安装驱动程序Ex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
