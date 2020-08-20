---
description: 以编程方式为 dBASE 驱动程序设置选项
title: 以编程方式为 dBASE 驱动程序设置选项 |Microsoft Docs
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
ms.openlocfilehash: 7c4b86b8284ca9a47e3ad40b1680a362035a3f13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471579"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以编程方式为 dBASE 驱动程序设置选项

|选项|说明|方法|  
|------------|-----------------|------------|  
|大约行计数|确定表大小统计信息是否近似。 此选项适用于使用 ODBC 驱动程序的所有数据源。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)时使用**STATISTICS**关键字。|  
|排序顺序|字段的排序顺序。<br /><br /> 序列可为： (默认) 或国际的 ASCII。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**COLLATINGSEQUENCE**关键字。|  
|数据源名称|标识数据源的名称，如工资单或人员。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)时使用**DSN**关键字。|  
|数据库|无需选择或创建数据库即可设置 Microsoft Access 数据源。 如果在安装过程中未提供任何数据库，则在用户连接到数据源时，系统将提示用户选择数据库文件。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**DBQ**关键字。|  
|描述|数据源中数据的可选说明;例如，"雇用日期、薪金历史记录和所有员工的当前评论"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**DESCRIPTION**关键字。|  
|排他|如果选择了 " **独占** " 框，则数据库将在独占模式下打开，一次只能由一个用户访问。 当在独占模式下运行时，性能会得到增强。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**EXCLUSIVE**关键字。|  
|页面超时|指定页 (如果未使用，则为页如果未使用，则在删除之前) 保留在缓冲区中。 默认值为 600 (60 秒) 的十分之几秒。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 由于固有的延迟，页面超时值不能为0。 页面超时值不能小于固有的延迟，即使页面超时选项设置在该值的下面也是如此。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**PAGETIMEOUT**关键字。|  
|只读|将数据库指定为只读。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)时使用**READONLY**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时，请指定最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，请将这些文件复制到此目录中。 或者，您可以使用目录名称在 SELECT 语句中限定文件名：<br /><br /> \*从 C:\MYDIR\EMP 中选择<br /><br /> 或者，您可以通过将 **SQLSetConnectOption** 函数与 SQL_CURRENT_QUALIFIER 选项一起使用来指定新的默认目录。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**DEFAULTDIR**关键字。|  
|显示删除的行|指定是否可以检索或定位已标记为已删除的行。 如果清除，则不会显示已删除的行;如果选择此选项，则会将已删除的行视为与非删除行相同。 默认情况下清除此复选框。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的调用中使用**DELETED**关键字。|
