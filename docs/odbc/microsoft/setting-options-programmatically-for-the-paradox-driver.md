---
title: 以编程方式为 Paradox 驱动程序设置选项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 658d03469e2733b0c25513a4d4a89c6ab88b9852
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063516"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以编程方式为 Paradox 驱动程序设置选项

|选项|说明|方法|  
|------------|-----------------|------------|  
|Directory|设置目标目录。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**DEFAULTDIR**关键字。|  
|排序顺序|字段的排序顺序。<br /><br /> 序列可以是 ASCII （默认值）、国际、瑞典语或挪威语-丹麦语。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**COLLATINGSEQUENCE**关键字。|  
|说明|数据源中数据的可选说明;例如，"雇用日期、薪金历史记录和所有员工的当前评论"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**DESCRIPTION**关键字。|  
|排他|如果选择了 "**独占**" 框，则数据库将在独占模式下打开，一次只能由一个用户访问。 在独占模式下运行时，性能得到了增强。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**EXCLUSIVE**关键字。|  
|Net 样式|访问 Paradox 数据时使用的网络访问样式： "*4.x" 表示*paradox 为3。*x*或 "4。*x*"（对于 Paradox 4）。*x*或5。*x*。 可以设置为 "3"。*x*"或" 4。如果版本为4，则为*x*。*x*或5。*x*;如果版本为 "Paradox 3"。*x*，样式必须为 "3"。*x*"。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**PARADOXNETSTYLE**关键字。|  
|页面超时|指定在删除之前页（如果未使用）保留在缓冲区中的时间段（以十分之一为一秒）。 默认值为600，即十分之一秒（60秒）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 由于固有的延迟，页面超时值不能为0。 页面超时值不能小于固有的延迟，即使页面超时选项设置在该值的下面也是如此。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**PAGETIMEOUT**关键字。|  
|只读|将数据库指定为只读。|若要动态设置此选项，请在调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)时使用**READONLY**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时，指定最常使用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，请将这些文件复制到此目录中。 或者，您可以使用目录名称在 SELECT 语句中限定文件名：<br /><br /> 从\* C:\MYDIR\EMP 中选择<br /><br /> 或者，您可以通过将**SQLSetConnectOption**函数与 SQL_CURRENT_QUALIFIER 选项一起使用来指定新的默认目录。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**DEFAULTDIR**关键字。|  
|选择网络目录|包含 Paradox lock 数据库的目录的完整路径，因为它包含 Pdoxusrs.net 文件（在 Paradox 4 中）。*x*）或 Paradox.net 文件（在 Paradox 5 中。*x*）。 如果目录不包含这些文件中的一个，则 Paradox 驱动程序会创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 你必须在 "**用户名**" 文本框中输入 Paradox 用户名，然后才能选择网络目录。 单击 "**选择网络目录**" 以选择网络目录。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**PARADOXNETPATH**关键字。|  
|用户名|Paradox 用户名。 当遇到锁定时，会向 Paradox 文件的其他用户显示此名称。|若要动态设置此选项，请在对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中使用**PARADOXUSERNAME**关键字。|
