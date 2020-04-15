---
title: 以编程方式设置文本文件驱动程序的选项 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300747"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>以编程方式为文本文件驱动程序设置选项

|选项|描述|方法|  
|------------|-----------------|------------|  
|数据源名称|标识数据源的名称，如工资单或人员。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)中的**DSN**关键字。|  
|定义格式|显示 **"定义文本格式"** 对话框，并使您能够在数据源目录中指定各个表的架构。|此选项不能通过调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)动态设置。|  
|描述|数据源中数据的可选说明;例如，"雇用日期、工资历史记录和所有员工的当前审核。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)调用中的 **"描述**"关键字。|  
|目录|选择目标目录。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中的**DEFAULTDIR**关键字。|  
|扩展列表|列出数据源上文本文件的文件名扩展名。 使用 Text 驱动程序时，当使用没有扩展名的名称执行 CREATE TABLE 语句时，将创建一个没有扩展名的文件。 其他驱动程序在未提供扩展名时创建具有默认扩展名的文件。 要创建具有 .txt 扩展名的文件，必须将扩展名包含在名称中。 要在 **"定义文本格式"** 对话框"*"中显示没有扩展名的文件。 必须添加到扩展列表中。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中的 **"扩展S"** 关键字。|  
|只读|将数据库指定为只读数据库。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中的**READONLY**关键字。|  
|要扫描的行|要扫描以确定每列数据类型的行数。 给定找到的最大数据类型数，确定数据类型。 如果遇到的数据与为列猜到的数据类型不匹配，则数据类型将作为 NULL 值返回。<br /><br /> 对于 Text 驱动程序，您可以输入从 1 到 32767 的数字，以便扫描的行数;但是，该值将始终默认为 25。 （超出限制的数字将返回错误。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)中的**MAXSCANROWS**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时，指定最常用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，则将其复制到此目录中。 或者，您可以在 SELECT 语句中限定具有目录名称的文件名：`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者，您可以使用**SQLSetConnectOption**函数使用SQL_CURRENT_QUALIFIER选项来指定新的默认目录。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中的**DEFAULTDIR**关键字。|
