---
title: 为 dBASE 驱动程序选项以编程方式设置 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcff8e5aefcd3ea810aae31d933cad14bc7541ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以编程方式设置 dBASE 驱动程序的选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|估计行数|确定是否近似表大小统计信息。 此选项适用于使用 ODBC 驱动程序的所有数据源。|若要动态设置此选项，使用**统计信息**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|排序规则序列|字段的排序顺序的序列。<br /><br /> 序列可以是： ASCII （默认值） 或 International。|若要动态设置此选项，使用**COLLATINGSEQUENCE**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|数据源名称|用于标识数据源，例如工资单或人员的名称。|若要动态设置此选项，使用**DSN**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|数据库|而无需选择或创建数据库，可以设置 Microsoft Access 数据源。 如果没有数据库在安装程序时提供的则将提示用户在连接到数据源时选择数据库文件。|若要动态设置此选项，使用**DBQ**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇用日期、 薪金历史记录和当前查看的所有雇员。"|若要动态设置此选项，使用**说明**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|排他|如果**独占**框为选中状态，数据库将以独占方式打开并将一次只能有一个用户可以访问。 它以独占模式运行时，得到增强性能。|若要动态设置此选项，使用**独占**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|页超时|以十分之一秒，缓冲区中保留的页 （如果未使用），移除之前指定的时间，段。 默认值为 600 秒 （60 秒） 的十分之几。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 页超时不能为 0，由于固有的延迟。 页超时不能早于固有的延迟，即使页 timeout 选项设置为低于该值的过程。|若要动态设置此选项，使用**PAGETIMEOUT**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|只读|将数据库指定为只读的。|若要动态设置此选项，使用**READONLY**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|选择目录|显示一个对话框，你可以在其中选择包含你想要访问的文件的目录。<br /><br /> 在定义数据源目录时，指定您最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 将其他文件复制到此目录中，如果经常使用它们。 或者，可以限定在 SELECT 语句以目录名称的文件名称：<br /><br /> 选择\*从 C:\MYDIR\EMP<br /><br /> 或者，你可以通过指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|显示已删除的行|指定是否可以检索或位于已标记为删除的行。 如果清除，则不会显示已删除的行;如果选中，将被视为已删除的行与非删除行相同。 默认情况下清除此复选框。|若要动态设置此选项，使用**已删除**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|
