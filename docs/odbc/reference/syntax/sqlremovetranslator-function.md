---
title: SQL删除转换器功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301784"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLRemove 翻译器**从系统信息的 Odbcinst.ini 部分中删除有关转换器的信息，并将转换器的组件使用量计数减少 1。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpsz 翻译*  
 [输入]在系统信息的 Odbcinst.ini 密钥中注册的翻译人员的姓名。  
  
 *lpdwUsageCount*  
 [输出]调用此函数后转换器的使用计数。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。 如果在调用此函数时系统信息中不存在条目，则函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemove 转换器**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|注册表中找不到组件|安装程序无法删除转换器信息，因为它要么不存在在注册表中，要么在注册表中找不到。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpsz 转换器*参数无效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法增加或递减组件使用量计数|安装程序未能减少驱动程序的使用计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLRemove 转换器**补充[SQLInstall 翻译器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)功能，并更新系统信息中的组件使用情况计数。 应仅从设置应用程序调用此功能。  
  
 **SQLRemove 转换器**将组件使用计数减少 1。 如果组件使用计数为 0，则系统信息中的转换器条目将被删除。 转换器条目位于系统信息中的以下位置，以转换器名称命名：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemove 转换器**实际上不会删除任何文件。 调用程序负责删除文件和维护文件使用情况计数。 只有在组件使用计数和文件使用计数都达到零后，才会物理删除文件。 组件中的某些文件可以删除，而其他文件不会删除，具体取决于其他应用程序是否使用文件，这些应用程序增加了文件使用量计数。  
  
 **SQLRemove 转换器**也称为升级过程的一部分。 如果应用程序检测到必须执行升级，并且以前已安装驱动程序，则应删除驱动程序，然后重新安装驱动程序。 应首先调用**SQLRemove 转换器**来递减组件使用计数，然后调用**SQLInstall 翻译器Ex**以增加组件使用计数。 应用程序安装程序必须用新文件物理替换旧文件。 文件使用情况计数将保持不变，使用旧版本文件的其他应用程序现在将使用较新版本。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|安装翻译器|[SQL安装翻译器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
