---
title: 安装程序 DLL 函数摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecb486f51caa97c715d54885c34575a60bfdfb83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231844"
---
# <a name="installer-dll-function-summary"></a>安装程序 DLL 函数摘要
下表介绍在安装程序 DLL 的函数。 有关语法和语义为每个函数的详细信息，请参阅[安装程序 DLL API 参考](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)。  
  
|任务|函数名称|用途|  
|----------|-------------------|-------------|  
|安装 ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|加载特定于驱动程序安装程序 DLL。|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|返回安装驱动程序的列表。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|将驱动程序添加到系统信息。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|返回目标目录的驱动程序管理器。|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|返回安装程序函数的错误或状态信息。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|将翻译添加到系统信息。|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|允许报告错误的驱动程序或转换器安装程序库。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|从系统信息中删除驱动程序。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|从系统信息中删除 ODBC 核心组件。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|从系统信息中删除转换器。|  
|配置数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|调用特定于驱动程序安装程序 DLL。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|显示一个对话框来添加数据源。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|检索指示列出 DSN 的值的 Odbc.ini 项所在的系统信息中的配置模式。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|将值写入系统信息。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|显示一个对话框来选择转换器。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|显示一个对话框来配置数据源和驱动程序。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|从文件 Dsn 中读取信息。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|删除默认数据源。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|删除数据源。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|设置指示列出 DSN 的值的 Odbc.ini 项所在的系统信息中的配置模式。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|长度和数据源名称的有效性检查。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|添加数据源。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|将信息写入到文件 Dsn。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|获取一个值中的系统信息。|
