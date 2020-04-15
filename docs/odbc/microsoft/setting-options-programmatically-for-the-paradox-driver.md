---
title: 以编程方式设置悖论驱动程序的选项 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d04de1f0de4baca5b3f474ef9fbcf3f886e6906f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300757"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以编程方式为 Paradox 驱动程序设置选项

|选项|描述|方法|  
|------------|-----------------|------------|  
|目录|设置目标目录。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中的**DEFAULTDIR**关键字。|  
|整理序列|字段排序的顺序。<br /><br /> 序列可以是 ASCII（默认值）、国际、瑞典-芬兰语或挪威-丹麦语。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)中的**COLLATINGSEQUENCE**关键字。|  
|描述|数据源中数据的可选说明;例如，"雇用日期、工资历史记录和所有员工的当前审核。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)调用中的 **"描述**"关键字。|  
|排他|如果选择了 **"独占"** 框，则数据库将在独占模式下打开，并且一次只能由一个用户访问。 在独占模式下运行时，性能会增强。|要动态设置此选项，请使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)调用中的**EXCLUSIVE**关键字。|  
|净样式|访问悖论数据时要使用的网络访问样式："3.x"，*x*表示悖论 3。*x*或"4。*x"* 为悖论4。*x*或 5。*x*. . 可以设置为"3"。*x"* 或"4。*x"* 如果版本是悖论4。*x*或 5。*x;* 如果版本是悖论 3。*x*，样式必须为"3"。*x"。*|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中的**PARADOXNETSTYLE**关键字。|  
|页面超时|指定页面（如果不使用）在删除之前保留在缓冲区中的时间段（以十分之一秒表示）。 默认值为 600 秒（60 秒）。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 由于固有的延迟，页面超时不能为 0。 即使页面超时选项设置为低于该值，页面超时也不能小于固有的延迟。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)中的**PAGETIMEOUT**关键字。|  
|只读|将数据库指定为只读数据库。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中的**READONLY**关键字。|  
|选择目录|显示一个对话框，您可以在其中选择包含要访问的文件的目录。<br /><br /> 定义数据源目录时，指定最常用的文件所在的目录。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用其他文件，则将其复制到此目录中。 或者，您可以在 SELECT 语句中限定具有目录名称的文件名：<br /><br /> 从\*C 选择：[MYDIR_EMP<br /><br /> 或者，您可以使用**SQLSetConnectOption**函数使用SQL_CURRENT_QUALIFIER选项来指定新的默认目录。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中的**DEFAULTDIR**关键字。|  
|选择网络目录|包含 Paradox 锁数据库的目录的完整路径，因为它包含Pdoxusrs.net文件（在悖论 4 中）。*x*） 或Paradox.net文件（在悖论 5 中）。*x*）。 如果目录不包含这些文件之一，则 Paradox 驱动程序将创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 在选择网络目录之前，必须在**用户名**文本框中输入 Paradox 用户名。 单击 **"选择网络目录**"以选择网络目录。|要动态设置此选项，请使用对[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的调用中的**PARADOXNETPATH**关键字。|  
|用户名|悖论用户名。 这是遇到锁时向 Paradox 文件的其他用户显示的名称。|要动态设置此选项，请使用调用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)中的**PARADOXUSERNAME**关键字。|
