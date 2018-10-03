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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c62503611e88435b139a00b180d3e087769b7fda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786576"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以编程方式为 Excel 驱动程序设置选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，请使用**DSN**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|“数据库”|Microsoft Access 数据源可以设置而无需选择或创建数据库。 如果在安装程序时未不提供任何数据库，将提示用户连接到数据源时选择的数据库文件。|若要动态设置此选项，请使用**DBQ**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇佣日期、 发薪记录和当前查看的所有员工。"|若要动态设置此选项，请使用**描述**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|目录|显示当前所选的目录。<br /><br /> 对于 Microsoft Excel 3.0/4.0 的文件，路径显示标记为"Directory"，为 Microsoft Excel 5.0 7.0 版，或 97 文件路径显示为标记为"工作簿"。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|只读|指定数据库为只读的。|若要动态设置此选项，请使用**READONLY**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|扫描的行数|要扫描以确定每个列的数据类型的行数。 数据类型确定给定类型的发现数据的最大数目。 如果遇到猜测的列的数据类型不匹配的数据，将作为 NULL 值返回的数据类型。<br /><br /> Microsoft Excel 驱动程序，您可以输入介于 1 到 16 个要扫描的行。 默认值为 8;如果设置为 0，将扫描所有行。 （限制以外的数字将返回错误。）|若要动态设置此选项，请使用**MAXSCANROWS**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|选择目录|显示一个对话框，您可以在其中选择包含想要访问的文件的目录。<br /><br /> 在定义数据源目录 （适用于 Microsoft 访问权限以外的所有驱动程序） 时，指定您最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用，请将其他文件复制到此目录。 或者，可以限定 SELECT 语句中使用的目录名称的文件名称：<br /><br /> 选择\*从 C:\MYDIR\EMP<br /><br /> 或者，你可以通过使用指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。<br /><br /> 对于 Microsoft Excel 3.0 或 4.0 文件，路径显示标记为"Directory"和路径选择按钮标记为"选择目录"。 Microsoft Excel 5.0、 7.0、 或 97 文件的路径显示标记为"工作簿"和路径选择按钮标记为"选择工作簿"。 在定义数据源目录时，指定您最常使用的 Microsoft Excel 文件的 Microsoft Excel 3.0/4.0，所在的目录或 Microsoft excel 5.0、 7.0、 或 97 所在的工作簿文件的目录。 **使用当前目录**禁用 Microsoft excel 5.0、 7.0 和 97。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|
