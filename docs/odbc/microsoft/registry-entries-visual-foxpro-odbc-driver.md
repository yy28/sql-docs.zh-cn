---
title: 注册表项 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de287802693adb18e39509fdc0e7577d05984949
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766545"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>注册表项（Visual FoxPro ODBC 驱动程序）
在安装 Visual FoxPro ODBC 驱动程序时，安装程序更新您的系统注册表中，在注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini，添加名为 Microsoft Visual FoxPro 驱动程序的新项。 在该注册表项，添加下表中描述的值。  
  
|值名称|值类型|ReplTest1|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|驱动程序|REG_SZ|Vfpodbc.dll 文件系统路径|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|安装|REG_SZ|Vfpodbc.dll 文件系统路径|  
|SQLLevel|REG_SZ|"0"|  
  
 安装程序还将添加"Visual FoxPro 文件"，表示默认 Visual FoxPro 驱动程序，到系统的 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 密钥的密钥。 此项下，安装程序将添加下表中描述的值。  
  
|值名称|值类型|ReplTest1|  
|----------------|----------------|-----------|  
|驱动程序|REG_SZ|Vfpodbc.dll 文件系统路径|  
  
 将 Visual FoxPro ODBC 数据源添加到您的 ODBC 配置，每次添加新的密钥为该数据源名称。 数据源的值中设置的值对应**ODBC Visual FoxPro 设置**对话框，如以下表中列出。  
  
|值名称 （关键字）|值类型|ReplTest1|  
|----------------------------|----------------|-----------|  
|逐份打印|REG_SQ|任何受支持的排序规则序列|  
|Description|REG_SZ|数据源的用户说明|  
|驱动程序||Vfpodbc.dll 文件系统路径|  
|排他||是或否|  
|BackgroundFetch||是或否|  
|SourceDB|REG_SZ|路径。DBC 文件|  
|SourceType|REG_SZ|"DBC"或者"DBF"|  
  
 不应直接调用访问此信息在添加、 修改或删除数据源时，注册表的任何管理被处理 ODBC 管理器。  
  
 可以使用其中的某些关键字和值作为中的参数[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函数。
