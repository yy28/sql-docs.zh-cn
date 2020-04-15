---
title: 安装程序 DLL 功能摘要 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddaf20334a84833433961a49e17724d354945c5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298767"
---
# <a name="installer-dll-function-summary"></a>安装程序 DLL 函数摘要
下表描述了安装程序 DLL 中的函数。 有关每个函数的语法和语义的详细信息，请参阅[安装程序 DLL API 参考](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)。  
  
|任务|函数名称|目标|  
|----------|-------------------|-------------|  
|安装 ODBC|[SQL 配置驱动程序](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|加载特定于驱动程序的安装程序 DLL。|  
||[SQLGet 安装驱动程序](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|返回已安装驱动程序的列表。|  
||[SQL安装驱动程序Ex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|向系统信息添加驱动程序。|  
||[SQLInstall驱动程序管理器](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|返回驱动程序管理器的目标目录。|  
||[SQL 安装程序错误](../../../odbc/reference/syntax/sqlinstallererror-function.md)|返回安装程序函数的错误或状态信息。|  
||[SQL安装翻译器Ex](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|向系统信息添加转换器。|  
||[SQLPost安装程序错误](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|允许驱动程序或转换器设置库报告错误。|  
||[SQL 删除驱动程序](../../../odbc/reference/syntax/sqlremovedriver-function.md)|从系统信息中删除驱动程序。|  
||[SQL删除驱动程序管理器](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|从系统信息中删除 ODBC 核心组件。|  
||[SQL 删除转换器](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|从系统信息中删除转换器。|  
|配置数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|调用特定于驱动程序的安装程序 DLL。|  
||[SQLCreate数据源](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|显示一个对话框以添加数据源。|  
||[SQLGet 配置模式](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|检索指示 Odbc.ini 条目列表 DSN 值在系统信息中的位置的配置模式。|  
||[SQLGet 私人配置文件字符串](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|向系统信息写入值。|  
||[SQLGet 转换器](../../../odbc/reference/syntax/sqlgettranslator-function.md)|显示要选择译员的对话框。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|显示用于配置数据源和驱动程序的对话框。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|从文件 DSN 读取信息。|  
||[SQL 删除默认数据源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|删除默认数据源。|  
||[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|删除数据源。|  
||[SQLSet 配置模式](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|设置配置模式，指示 Odbc.ini 条目列表 DSN 值在系统信息中的位置。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|检查数据源名称的长度和有效性。|  
||[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|添加数据源。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|将信息写入文件 DSN。|  
||[SQLWrite 私有配置文件字符串](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|从系统信息获取值。|
