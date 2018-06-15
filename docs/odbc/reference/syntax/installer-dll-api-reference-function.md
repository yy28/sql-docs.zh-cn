---
title: 安装程序 DLL API 参考函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installer DLL [ODBC]
ms.assetid: 47fcadc3-f102-4989-9ee7-a1c65233142a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37828082300c387ac6a421171ca6fefaa0a2cad1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916912"
---
# <a name="installer-dll-api-reference-function"></a>安装程序 DLL API 参考函数
本部分介绍在安装程序 DLL API 函数的语法。 安装程序 DLL API 包含 20 函数。 这些函数的三个**SQLGetTranslator**， **SQLRemoveDSNFromIni**，和**SQLWriteDSNToIni**，只能由安装程序 Dll 调用。 其他函数所调用的设置和管理程序。  
  
 每个函数都标有在其中引入的 ODBC 的版本。  
  
 本部分包含以下主题。  
  
-   [SQLConfigDataSource 函数](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)  
  
-   [SQLConfigDriver 函数](../../../odbc/reference/syntax/sqlconfigdriver-function.md)  
  
-   [SQLCreateDataSource 函数](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)  
  
-   [SQLGetConfigMode 函数](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)  
  
-   [SQLGetInstalledDrivers 函数](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)  
  
-   [SQLGetPrivateProfileString 函数](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)  
  
-   [SQLGetTranslator 函数](../../../odbc/reference/syntax/sqlgettranslator-function.md)  
  
-   [SQLInstallDriverEx 函数](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)  
  
-   [SQLInstallDriverManager 函数](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)  
  
-   [SQLInstallerError 函数](../../../odbc/reference/syntax/sqlinstallererror-function.md)  
  
-   [SQLInstallTranslator 函数](../../../odbc/reference/syntax/sqlinstalltranslator-function.md)  
  
-   [SQLInstallTranslatorEx 函数](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)  
  
-   [SQLManageDataSources 函数](../../../odbc/reference/syntax/sqlmanagedatasources.md)  
  
-   [SQLPostInstallerError 函数](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)  
  
-   [SQLReadFileDSN 函数](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)  
  
-   [SQLRemoveDefaultDataSource 函数](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)  
  
-   [SQLRemoveDriver 函数](../../../odbc/reference/syntax/sqlremovedriver-function.md)  
  
-   [SQLRemoveDriverManager 函数](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)  
  
-   [SQLRemoveDSNFromIni 函数](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)  
  
-   [SQLRemoveTranslator 函数](../../../odbc/reference/syntax/sqlremovetranslator-function.md)  
  
-   [SQLSetConfigMode 函数](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)  
  
-   [SQLValidDSN 函数](../../../odbc/reference/syntax/sqlvaliddsn-function.md)  
  
-   [SQLWriteDSNToIni 函数](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)  
  
-   [SQLWriteFileDSN 函数](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)  
  
-   [SQLWritePrivateProfileString 函数](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)
