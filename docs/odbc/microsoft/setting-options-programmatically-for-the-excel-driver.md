---
title: 以编程方式设置 Excel 驱动程序的选项 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fcd5542e4beee1f7c7a30d5e0ee9f2815a3f0b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300767"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以编程方式为 Excel 驱动程序设置选项

|选项|描述|方法|  
|------------|-----------------|------------|  
|数据源名称|标识数据源的名称，如工资单或人员。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)中的**DSN**关键字。|  
|数据库|无需选择或创建数据库即可设置 Microsoft Access 数据源。 如果在设置时未提供数据库，则在连接到数据源时将提示用户选择数据库文件。|要动态设置此选项，请使用**DBQ**关键字调用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|描述|数据源中数据的可选说明;例如，"雇用日期、工资历史记录和所有员工的当前审核。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)调用中的 **"描述**"关键字。|  
|目录|显示当前选定的目录。<br /><br /> 对于 Microsoft Excel 3.0/4.0 文件，路径显示标记为"目录"，而对于 Microsoft Excel 5.0、7.0 或 97 个文件，路径显示标记为"工作簿"。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中的**DEFAULTDIR**关键字。|  
|只读|将数据库指定为只读数据库。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中的**READONLY**关键字。|  
|要扫描的行|要扫描以确定每列数据类型的行数。 给定找到的最大数据类型数，确定数据类型。 如果遇到的数据与为列猜到的数据类型不匹配，则数据类型将作为 NULL 值返回。<br /><br /> 对于 Microsoft Excel 驱动程序，可以输入从 1 到 16 的数字，以便对行进行扫描。 该值默认为 8;如果设置为 0，则扫描所有行。 （超出限制的数字将返回错误。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)中的**MAXSCANROWS**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时（对于除 Microsoft Access 之外的所有驱动程序），指定最常用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，则将其复制到此目录中。 或者，您可以在 SELECT 语句中限定具有目录名称的文件名：<br /><br /> 从\*C 选择：[MYDIR_EMP<br /><br /> 或者，您可以使用**SQLSetConnectOption**函数使用SQL_CURRENT_QUALIFIER选项来指定新的默认目录。<br /><br /> 对于 Microsoft Excel 3.0 或 4.0 文件，路径显示标记为"目录"，路径选择按钮标记为"选择目录"。 对于 Microsoft Excel 5.0、7.0 或 97 个文件，路径显示标记为"工作簿"，路径选择按钮标记为"选择工作簿"。 定义数据源目录时，请指定最常用的 Microsoft Excel 文件位于 Microsoft Excel 3.0/4.0 的目录，或为 Microsoft Excel 5.0、7.0 或 97 提供工作簿文件的目录。 对于 Microsoft Excel 5.0、7.0 和 97，禁用了 **"当前目录**"。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中的**DEFAULTDIR**关键字。|
