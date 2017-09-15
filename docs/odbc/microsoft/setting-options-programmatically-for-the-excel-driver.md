---
title: "以编程方式为 Excel 驱动程序设置选项 |Microsoft 文档"
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
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da1f2ed6bbca3709c8223713f4841ed34288f5a3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以编程方式为 Excel 驱动程序的的设置选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，使用**DSN**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|数据库|而无需选择或创建数据库，可以设置 Microsoft Access 数据源。 如果没有数据库在安装程序时提供的则将提示用户能够连接到数据源时选择某个数据库文件。|若要动态设置此选项，使用**DBQ**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇用日期、 薪金历史记录和当前查看的所有雇员。"|若要动态设置此选项，使用**说明**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|目录|显示当前所选的目录。<br /><br /> Microsoft Excel 3.0/4.0 文件的路径显示标记为"Directory"，为 Microsoft Excel 5.0，7.0，或 97 文件的路径显示标记为"工作簿"。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|只读|将数据库指定为只读的。|若要动态设置此选项，使用**READONLY**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|扫描的行数|要扫描以确定每个列的数据类型的行数。 考虑到的类型的发现数据的最大数目确定的数据类型。 如果遇到数据猜测的列的数据类型不匹配，则将为 NULL 值返回的数据类型。<br /><br /> Microsoft Excel 驱动程序，你可以输入一个介于 1 到 16 个要扫描的行。 默认值为 8;如果设置为 0，将扫描所有行。 （限制以外的数字将返回错误。）|若要动态设置此选项，使用**MAXSCANROWS**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|选择目录|显示一个对话框，你可以在其中选择包含你想要访问的文件的目录。<br /><br /> 在定义的数据源目录 （除 Microsoft Access 的所有驱动程序） 时，指定你最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 将其他文件复制到此目录中，如果经常使用它们。 或者，可以限定在 SELECT 语句以目录名称的文件名称：<br /><br /> 选择\*从 C:\MYDIR\EMP<br /><br /> 或者，你可以通过指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。<br /><br /> 对于 Microsoft Excel 3.0 或 4.0 文件，路径显示标记为"Directory"和路径选择按钮标记为"选择目录"。 Microsoft Excel 5.0、 7.0 或 97 文件的路径显示标记为"工作簿"和路径选择按钮标记为"选择工作簿"。 在定义数据源目录时，指定你最常使用的 Microsoft Excel 文件所在的 Microsoft Excel 3.0/4.0，目录或 Microsoft excel 5.0、 7.0 或 97 所在的工作簿文件的目录。 **使用当前目录**禁用 Microsoft excel 5.0、 7.0 和 97。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|
