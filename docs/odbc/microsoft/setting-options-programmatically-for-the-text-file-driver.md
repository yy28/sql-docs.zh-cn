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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300747"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>以编程方式为文本文件驱动程序设置选项

|选项|说明|方法|  
|------------|-----------------|------------|  
|数据源名称|标识数据源的名称，如工资单或人员。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)时使用**DSN**关键字。|  
|定义格式|显示 "**定义文本格式**" 对话框，并使您能够指定数据源目录中各个表的架构。|此选项不能通过调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)进行动态设置。|  
|说明|数据源中数据的可选说明;例如，"雇用日期、薪金历史记录和所有员工的当前评论"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中使用**DESCRIPTION**关键字。|  
|目录|选择目标目录。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中使用**DEFAULTDIR**关键字。|  
|扩展列表|列出数据源上的文本文件的文件扩展名。 使用文本驱动程序时，如果使用没有扩展名的名称执行 CREATE TABLE 语句，则将创建不带扩展名的文件。 当未提供扩展时，其他驱动程序将使用默认扩展名创建一个文件。 若要创建扩展名为 .txt 的文件，必须在名称中包含扩展名。 若要在 "**定义文本格式**" 对话框中显示不带扩展名的文件，请 "*"。 必须添加到 "扩展" 列表中。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中使用**extension**关键字。|  
|只读|将数据库指定为只读。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)时使用**READONLY**关键字。|  
|要扫描的行|要扫描以确定每个列的数据类型的行数。 数据类型是根据找到的数据类型的最大数目确定的。 如果遇到的数据与对列推测的数据类型不匹配，则数据类型将返回为 NULL 值。<br /><br /> 对于文本驱动程序，您可以为要扫描的行数输入1到32767之间的一个数字;但是，值始终默认为25。 （超出限制的数字将返回错误。）|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中使用**MAXSCANROWS**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时，指定最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，请将这些文件复制到此目录中。 或者，您可以使用目录名称在 SELECT 语句中限定文件名：`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者，您可以通过将**SQLSetConnectOption**函数与 SQL_CURRENT_QUALIFIER 选项一起使用来指定新的默认目录。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的调用中使用**DEFAULTDIR**关键字。|
