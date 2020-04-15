---
title: 注册表条目（可视化福克斯Pro ODBC驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd2d419a94c45a872789e095b014159b41d7c217
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304834"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>注册表项（Visual FoxPro ODBC 驱动程序）
安装 Visual FoxPro ODBC 驱动程序时，安装程序在注册表HKEY_LOCAL_MACHINE_SOFTWARE_ODBC_ODBCInst.ini 中更新系统的注册表，以添加新密钥，称为 Microsoft Visual FoxPro 驱动程序。 在该键下，将添加下表中描述的值。  
  
|值名称|值类型|“值”|  
|----------------|----------------|-----------|  
|API 级别|REG_SZ|“1”|  
|连接功能|REG_SZ|"YYN"|  
|驱动程序|REG_SZ|vfpodbc.dll 文件的系统路径|  
|DriverODBCVer|REG_SZ|"02.50"|  
|文件 Extns|REG_SZ|".dbf，\*.cdx，\*.fpt"|  
|文件使用|REG_SZ|“1”|  
|设置|REG_SZ|vfpodbc.dll 文件的系统路径|  
|SQLLevel|REG_SZ|"0"|  
  
 安装程序还将代表默认 Visual FoxPro 驱动程序的密钥"Visual FoxPro 文件"添加到系统的HKEY_CURRENT_USER_SOFTWARE_ODBC_Odbc.ini 密钥。 在此键下，安装程序将添加下表中描述的值。  
  
|值名称|值类型|“值”|  
|----------------|----------------|-----------|  
|驱动程序|REG_SZ|vfpodbc.dll 文件的系统路径|  
  
 每次将 Visual FoxPro ODBC 数据源添加到 ODBC 配置时，都会为该数据源名称添加新密钥。 数据源的值对应于您在**ODBC Visual FoxPro 安装程序**对话框中设置的值，如下表中列出的。  
  
|值名称（关键字）|值类型|“值”|  
|----------------------------|----------------|-----------|  
|逐份打印|REG_SQ|任何支持的整理序列|  
|描述|REG_SZ|数据源的用户描述|  
|驱动程序||vfpodbc.dll 文件的系统路径|  
|排他|| 是或否|  
|背景提取|| 是或否|  
|SourceDB|REG_SZ|到 的路径。DBC 文件|  
|SourceType|REG_SZ|"DBC"或"DBF"|  
  
 您不应直接访问此信息;因此，您不应直接访问此信息。当您添加、修改或删除数据源时，注册的任何管理将由 ODBC 管理员处理。  
  
 您可以在[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函数中将其中一些关键字和值用作参数。
