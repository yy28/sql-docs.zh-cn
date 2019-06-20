---
title: 为 dBASE 驱动程序选项以编程方式设置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a268e72262f9f8252ea89774876f3d04008fe4c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284949"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以编程方式为 dBASE 驱动程序设置选项

|Option|Description|方法|  
|------------|-----------------|------------|  
|估计行数|确定是否近似表大小统计信息。 此选项适用于使用 ODBC 驱动程序的所有数据源。|若要动态设置此选项，请使用**统计信息**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|对序列进行排序|字段的排序顺序的序列。<br /><br /> 序列可以是：ASCII （默认值） 或国际。|若要动态设置此选项，请使用**COLLATINGSEQUENCE**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，请使用**DSN**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|“数据库”|Microsoft Access 数据源可以设置而无需选择或创建数据库。 如果在安装程序时未不提供任何数据库，将提示用户在连接到数据源时选择数据库文件。|若要动态设置此选项，请使用**DBQ**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇佣日期、 发薪记录和当前查看的所有员工。"|若要动态设置此选项，请使用**描述**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|排他|如果**独占**框处于选中状态，数据库将以独占方式打开，并且一次只能有一个用户可以访问。 它在排他模式下运行时，性能得到了增强。|若要动态设置此选项，请使用**独占**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|页超时|指定时间，的段中的第二个，在移除之前，在缓冲区中会保留一页 （如果不使用） 的十分之几。 默认值为 600 秒 （60 秒） 的十分之几秒。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 页超时不能为 0，由于固有的延迟。 页超时不能早于固有的延迟，即使页面超时选项设置为低于该值。|若要动态设置此选项，请使用**PAGETIMEOUT**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|只读|指定数据库为只读的。|若要动态设置此选项，请使用**READONLY**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|选择目录|显示一个对话框，您可以在其中选择包含想要访问的文件的目录。<br /><br /> 在定义数据源目录时，指定您最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用，请将其他文件复制到此目录。 或者，可以限定 SELECT 语句中使用的目录名称的文件名称：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，你可以通过使用指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|显示已删除的行|指定是否可以检索或位于已标记为已删除的行。 如果未选中状态，不会显示已删除的行;如果选中，将被视为已删除的行与非删除行相同。 默认情况下清除此复选框。|若要动态设置此选项，请使用**DELETED**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|
