---
title: "以编程方式为文本文件驱动程序设置选项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1a7f971a0ac5d07c451b9a786bdcc563108e3f7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>以编程方式为文本文件驱动程序设置选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，使用**DSN**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|定义格式|显示**定义文本格式**对话框中，您可以指定在数据源目录中的各个表的架构。|此选项不能通过调用动态设置[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇用日期、 薪金历史记录和当前查看的所有雇员。"|若要动态设置此选项，使用**说明**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|目录|选择的目标的目录。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|扩展列表|列出数据源上的文本文件的文件扩展名。 当使用文本驱动程序时，执行 CREATE TABLE 语句时使用不具有扩展名的名称时创建不带扩展名的文件。 提供无扩展名时，其他驱动程序创建具有默认扩展插件的文件。 若要创建具有扩展名为.txt 的文件，必须在名称中包含扩展。 若要显示不带扩展中的文件**定义文本格式**对话框中，"*。" 必须添加到扩展列表。|若要动态设置此选项，使用**扩展**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|只读|将数据库指定为只读的。|若要动态设置此选项，使用**READONLY**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|扫描的行数|要扫描以确定每个列的数据类型的行数。 考虑到的类型的发现数据的最大数目确定的数据类型。 如果遇到数据猜测的列的数据类型不匹配，则将为 NULL 值返回的数据类型。<br /><br /> 文本驱动程序，你可能输入一个介于 1 到 32767 之间的要扫描; 的行数但是，此值将始终默认为 25。 （限制以外的数字将返回错误。）|若要动态设置此选项，使用**MAXSCANROWS**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|选择目录|显示一个对话框，你可以在其中选择包含你想要访问的文件的目录。<br /><br /> 介绍了当定义数据源目录指定你最常用文件的目录。 ODBC 驱动程序使用此目录作为默认目录。 将其他文件复制到此目录中，如果经常使用它们。 或者，可以限定在 SELECT 语句以目录名称的文件名称：`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者，你可以通过指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|
