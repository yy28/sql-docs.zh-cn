---
title: 以编程方式设置 dBASE 驱动程序的选项 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300777"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以编程方式为 dBASE 驱动程序设置选项

|选项|描述|方法|  
|------------|-----------------|------------|  
|近似行计数|确定表大小统计信息是否近似。 此选项适用于使用 ODBC 驱动程序的所有数据源。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)调用中的**STATISTICS**关键字。|  
|整理序列|字段排序的顺序。<br /><br /> 序列可以是：ASCII（默认值）或国际。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)中的**COLLATINGSEQUENCE**关键字。|  
|数据源名称|标识数据源的名称，如工资单或人员。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)中的**DSN**关键字。|  
|数据库|无需选择或创建数据库即可设置 Microsoft Access 数据源。 如果在设置时未提供数据库，则用户在连接到数据源时将提示他们选择数据库文件。|要动态设置此选项，请使用**DBQ**关键字调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|描述|数据源中数据的可选说明;例如，"雇用日期、工资历史记录和所有员工的当前审核。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)调用中的 **"描述**"关键字。|  
|排他|如果选择了 **"独占"** 框，则数据库将在独占模式下打开，并且一次只能由一个用户访问。 在独占模式下运行时，性能会增强。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)调用中的**EXCLUSIVE**关键字。|  
|页面超时|指定页面（如果不使用）在删除之前保留在缓冲区中的时间段（以十分之一秒表示）。 默认值为 600 秒（60 秒）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 由于固有的延迟，页面超时不能为 0。 即使页面超时选项设置为低于该值，页面超时也不能小于固有的延迟。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)中的**PAGETIMEOUT**关键字。|  
|只读|将数据库指定为只读数据库。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中的**READONLY**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时，请指定最常用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，则将其复制到此目录中。 或者，您可以在 SELECT 语句中限定具有目录名称的文件名：<br /><br /> 从\*C 选择：[MYDIR_EMP<br /><br /> 或者，您可以使用**SQLSetConnectOption**函数使用SQL_CURRENT_QUALIFIER选项来指定新的默认目录。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中的**DEFAULTDIR**关键字。|  
|显示已删除的行|指定是否可以检索或定位已标记为已删除的行。 如果清除，则不显示已删除的行;如果清除，则不显示已删除的行。如果选中，则删除的行将被视为与未删除的行相同。 默认情况下清除此复选框。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中的**DELETED**关键字。|
