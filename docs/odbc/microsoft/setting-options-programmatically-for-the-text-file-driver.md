---
title: 以编程方式为文本文件驱动程序设置选项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04bd9a37d87c91fe3f42cbb1fdf464660ba5a299
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044414"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>以编程方式为文本文件驱动程序设置选项

|选项|Description|方法|  
|------------|-----------------|------------|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，请使用**DSN**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|定义格式|显示**定义文本格式**对话框中，可用于指定数据源目录中为单独的表的架构。|此选项不能动态设置通过调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇佣日期、 发薪记录和当前查看的所有员工。"|若要动态设置此选项，请使用**描述**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|目录|选择目标的目录。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|扩展列表|列出数据源上的文本文件的文件名称扩展。 使用文本驱动程序时，使用不具有扩展名的名称执行 CREATE TABLE 语句时创建不带扩展名的文件。 提供没有扩展名时，其他驱动程序默认扩展名为创建一个文件。 若要创建具有.txt 扩展名的文件，必须在名称中包含扩展。 若要显示不带扩展中的文件**定义文本格式**对话框中，"*。" 必须添加到扩展列表。|若要动态设置此选项，请使用**扩展**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|只读|指定数据库为只读的。|若要动态设置此选项，请使用**READONLY**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|扫描的行数|要扫描以确定每个列的数据类型的行数。 数据类型确定给定类型的发现数据的最大数目。 如果遇到猜测的列的数据类型不匹配的数据，将作为 NULL 值返回的数据类型。<br /><br /> 文本驱动程序，您可以输入一个介于 1 到 32767 之间的要扫描; 的行数但是，值将始终默认为 25。 （限制以外的数字将返回错误。）|若要动态设置此选项，请使用**MAXSCANROWS**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|选择目录|显示一个对话框，您可以在其中选择包含想要访问的文件的目录。<br /><br /> 定义数据源目录时指定最常用文件的目录位于。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用，请将其他文件复制到此目录。 或者，可以限定 SELECT 语句中使用的目录名称的文件名称： `SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者，你可以通过使用指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|
