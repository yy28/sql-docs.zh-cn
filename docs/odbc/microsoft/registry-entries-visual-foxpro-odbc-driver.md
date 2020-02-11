---
title: 注册表项（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.openlocfilehash: 00a24ffca764c029b87470b7aa07d15f33b4c673
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996452"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>注册表项（Visual FoxPro ODBC 驱动程序）
安装 Visual FoxPro ODBC 驱动程序时，安装程序会更新系统的注册表，在注册表项 HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBCInst.ini 中，添加一个名为 Microsoft Visual FoxPro 驱动程序的新密钥。 在该注册表项下，将添加下表中描述的值。  
  
|值名称|值类型|值|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|“1”|  
|ConnectFunctions|REG_SZ|"YYN"|  
|驱动程序|REG_SZ|Vfpodbc 文件的系统路径|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"* .dbf、\*. cdx、\*. fpt"|  
|FileUsage|REG_SZ|“1”|  
|安装|REG_SZ|Vfpodbc 文件的系统路径|  
|SQLLevel|REG_SZ|"0"|  
  
 安装程序还会将表示默认 Visual FoxPro 驱动程序的密钥 "视觉 FoxPro 文件" 添加到系统的 HKEY_CURRENT_USER \SOFTWARE\ODBC\Odbc.ini 密钥。 在此项下，安装程序会添加下表中描述的值。  
  
|值名称|值类型|值|  
|----------------|----------------|-----------|  
|驱动程序|REG_SZ|Vfpodbc 文件的系统路径|  
  
 每次向 ODBC 配置中添加一个 Visual FoxPro ODBC 数据源时，将为该数据源名称添加一个新的键。 数据源的值对应于在 " **ODBC Visual FoxPro 设置**" 对话框中设置的值，如下表所示。  
  
|值名称（关键字）|值类型|值|  
|----------------------------|----------------|-----------|  
|逐份打印|REG_SQ|任何支持的排序顺序|  
|说明|REG_SZ|数据源的用户说明|  
|驱动程序||Vfpodbc 文件的系统路径|  
|排他||是或否|  
|BackgroundFetch||是或否|  
|SourceDB|REG_SZ|指向的路径。DBC 文件|  
|SourceType|REG_SZ|"DBC" 或 "DBF"|  
  
 不应直接访问此信息;添加、修改或删除数据源时，ODBC 管理员会处理注册表的任何管理。  
  
 可以在[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函数中将其中一些关键字和值用作参数。
