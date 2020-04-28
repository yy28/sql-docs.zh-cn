---
title: 以编程方式为 Excel 驱动程序设置选项 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300767"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以编程方式为 Excel 驱动程序设置选项

|选项|说明|方法|  
|------------|-----------------|------------|  
|数据源名称|标识数据源的名称，如工资单或人员。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)时使用**DSN**关键字。|  
|数据库|无需选择或创建数据库即可设置 Microsoft Access 数据源。 如果在安装过程中未提供任何数据库，则在连接到数据源时，系统将提示用户选择数据库文件。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中使用**DBQ**关键字。|  
|说明|数据源中数据的可选说明;例如，"雇用日期、薪金历史记录和所有员工的当前评论"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中使用**DESCRIPTION**关键字。|  
|目录|显示当前所选目录。<br /><br /> 对于 Microsoft Excel 3.0/4.0 文件，路径显示标志为 "Directory"，而对于 Microsoft Excel 5.0、7.0 或97文件，路径显示标为 "工作簿"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中使用**DEFAULTDIR**关键字。|  
|只读|将数据库指定为只读。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)时使用**READONLY**关键字。|  
|要扫描的行|要扫描以确定每个列的数据类型的行数。 数据类型是根据找到的数据类型的最大数目确定的。 如果遇到的数据与对列推测的数据类型不匹配，则数据类型将返回为 NULL 值。<br /><br /> 对于 Microsoft Excel 驱动程序，可以为要扫描的行输入一个介于1和16之间的数字。 该值默认为 8;如果设置为0，则扫描所有行。 （超出限制的数字将返回错误。）|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中使用**MAXSCANROWS**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录（对于除 Microsoft Access 之外的所有驱动程序），请指定最常用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，请将这些文件复制到此目录中。 或者，您可以使用目录名称在 SELECT 语句中限定文件名：<br /><br /> 从\* C:\MYDIR\EMP 中选择<br /><br /> 或者，您可以通过将**SQLSetConnectOption**函数与 SQL_CURRENT_QUALIFIER 选项一起使用来指定新的默认目录。<br /><br /> 对于 Microsoft Excel 3.0 或4.0 文件，路径显示标记为 "Directory"，路径选择按钮标记为 "选择目录"。 对于 Microsoft Excel 5.0、7.0 或97文件，路径显示标为 "工作簿"，路径选择按钮标记为 "选择工作簿"。 定义数据源目录时，请指定最常用的 Microsoft Excel 文件所在的目录，该目录中的 microsoft excel 3.0/4.0 或工作簿文件所在的目录用于 Microsoft Excel 5.0、7.0 或97。 Microsoft Excel 5.0、7.0 和97禁用了 "**使用当前目录**"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的调用中使用**DEFAULTDIR**关键字。|
