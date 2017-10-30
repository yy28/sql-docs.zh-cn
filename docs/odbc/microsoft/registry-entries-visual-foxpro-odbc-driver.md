---
title: "注册表项 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a975ff73eb4b2ef48af05ccfdf595ae9c3233f0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>注册表项 （Visual FoxPro ODBC 驱动程序）
在安装 Visual FoxPro ODBC 驱动程序时，安装程序将更新你的系统注册表中，注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini，添加新项称为 Microsoft Visual FoxPro 驱动程序中。 在该注册表项，添加以下表中描述的值。  
  
|值名称|值类型|值|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|驱动程序|REG_SZ|Vfpodbc.dll 文件系统路径|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf，\*.cdx，\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|安装|REG_SZ|Vfpodbc.dll 文件系统路径|  
|SQLLevel|REG_SZ|"0"|  
  
 安装程序还将添加"Visual FoxPro 文件"，表示默认 Visual FoxPro 驱动程序，对你的系统 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 密钥的密钥。 此项下的安装程序将添加下表中描述的值。  
  
|值名称|值类型|值|  
|----------------|----------------|-----------|  
|驱动程序|REG_SZ|Vfpodbc.dll 文件系统路径|  
  
 将 Visual FoxPro ODBC 数据源添加到您的 ODBC 配置，每次添加新的密钥对该数据源名称。 数据源值对应于在中设置的值**ODBC Visual FoxPro 安装**对话框中下, 表中列出。  
  
|值名称 （关键字）|值类型|值|  
|----------------------------|----------------|-----------|  
|逐份打印|REG_SQ|任何受支持的排序规则序列|  
|Description|REG_SZ|数据源的用户说明|  
|驱动程序||Vfpodbc.dll 文件系统路径|  
|排他||是或否|  
|BackgroundFetch||是或否|  
|SourceDB|REG_SZ|路径。DBC 文件|  
|SourceType|REG_SZ|"DBC"或者"DBF"|  
  
 不应直接调用访问此信息在添加、 修改或删除数据源时，任何管理注册表被处理由 ODBC 管理器。  
  
 可以使用其中的某些关键字和值中的参数一样[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 函数。

