---
title: SQLRemoveTranslator 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42513e6dcf32e21030e56fd3b386800b7525f534
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537152"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函数
**符合性**  
 版本引入了：ODBC 3.0  
  
 **摘要**  
 **SQLRemoveTranslator**有关转换器的信息从节中删除 Odbcinst.ini 的系统信息和递减的转换器的组件使用情况计数按 1。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpszTranslator*  
 [输入]转换器，因为注册中的系统信息 Odbcinst.ini 键的名称。  
  
 *lpdwUsageCount*  
 [输出]翻译后调用此函数的使用情况计数。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。 如果没有条目中的系统信息调用此函数时，该函数将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveTranslator**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序无法删除翻译信息，因为它在注册表中不存在或找不到注册表中。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszTranslator*参数无效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法递减的驱动程序的使用计数。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveTranslator**进行了补充[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)函数和更新组件使用情况的系统信息中的数。 只能从安装程序应用程序应调用此函数。  
  
 **SQLRemoveTranslator**将组件的使用情况计数递减 1。 如果组件使用情况计数达到 0，将删除的系统信息中的翻译条目。 转换器条目中下转换器名称的系统信息中的以下位置为：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator**不会实际删除任何文件。 调用程序负责删除文件，和维护文件使用情况计数。 组件使用情况计数和文件使用率计数已达到仅后零是以物理方式已删除的文件。 可以删除一个组件中的某些文件，并且其他人不会删除，具体取决于是否使用具有递增文件使用情况计数的其他应用程序的文件。  
  
 **SQLRemoveTranslator**也称为升级过程的一部分。 如果应用程序检测到它必须执行升级和它以前已安装的驱动程序，应删除并再重新安装该驱动程序。 **SQLRemoveTranslator**首先应调用要递减的组件使用计数，然后**SQLInstallTranslatorEx**应调用来增加的组件使用情况计数。 应用程序安装程序必须以物理方式旧的文件将替换为新文件。 文件使用情况计数将保持不变，并使用较旧版本文件的其他应用程序现在将使用较新版本。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|安装一个转换器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
