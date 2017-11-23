---
title: "SQLRemoveTranslator 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRemoveTranslator
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveTranslator
helpviewer_keywords: SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2275533c204c6c123edbfde8354615e6881e8730
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLRemoveTranslator**删除有关转换器信息 Odbcinst.ini 节中的系统信息和递减转换器的组件使用率计数 1。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpszTranslator*  
 [输入]转换器注册在系统信息的 Odbcinst.ini 键的名称。  
  
 *lpdwUsageCount*  
 [输出]转换器后调用此函数使用情况计数。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。 如果没有条目存在的系统信息中，调用此函数时，此函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveTranslator**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序无法删除转换器信息，因为它在注册表中不存在或无法在注册表中找到。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszTranslator*自变量无效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法减少该驱动程序的使用情况计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveTranslator**进行了补充[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)函数和更新的组件使用情况计数的系统信息。 只能从安装程序应用程序，应调用此函数。  
  
 **SQLRemoveTranslator**将按 1 递减的组件使用计数。 如果组件使用情况计数归为 0，则将删除的系统信息中的转换器条目。 转换器条目中的转换器名称下的系统信息中的以下位置为：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator**不会实际删除任何文件。 调用程序负责删除文件，并维护文件使用率计数。 仅的组件使用计数和文件使用率计数已达到后零是以物理方式删除的文件。 可以删除组件中的某些文件，并且其他人不会删除，具体取决于是否将使用文件的其他应用程序具有递增文件使用率计数。  
  
 **SQLRemoveTranslator**也称为升级过程的一部分。 如果应用程序检测到它已执行升级，以及它以前已安装该驱动程序，则应删除该驱动程序，并将其然后重新安装。 **SQLRemoveTranslator**首先应调用以递减的组件使用计数，然后**SQLInstallTranslatorEx**应调用以递增的组件使用计数。 应用程序安装程序必须以物理方式将新的文件替换旧的文件。 文件使用情况计数将保持不变，并使用以前版本的文件的其他应用程序现在将使用较新版本。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|安装一个转换器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
