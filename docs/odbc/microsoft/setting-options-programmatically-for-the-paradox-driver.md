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
manager: craigg
ms.openlocfilehash: fd92344552371e2e052a958485340b70522cc121
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313573"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以编程方式为 Paradox 驱动程序设置选项

|Option|Description|方法|  
|------------|-----------------|------------|  
|目录|设置的目标的目录。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|对序列进行排序|字段的排序顺序的序列。<br /><br /> 序列可以是 ASCII （默认值）、 国际、 瑞典语-芬兰语或挪威语-丹麦语。|若要动态设置此选项，请使用**COLLATINGSEQUENCE**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇佣日期、 发薪记录和当前查看的所有员工。"|若要动态设置此选项，请使用**描述**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|排他|如果**独占**框处于选中状态，数据库将以独占方式打开，并且一次只能有一个用户可以访问。 以独占模式运行时，性能得到了增强。|若要动态设置此选项，请使用**独占**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Net 样式|要访问 Paradox 数据时使用的网络访问样式： 任一"3。*x*"Paradox 3。*x*或"4。*x*"可能是 4。*x*或 5。*x*。 可以将设置为"3。*x*"或"4。*x*"如果版本可能是 4。*x*或 5。*x*; 如果版本为 Paradox 3。*x*，该样式必须是"3。*x*"。|若要动态设置此选项，请使用**PARADOXNETSTYLE**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|页超时|指定时间，的段中 （如果不使用） 会保留一页在缓冲区中被删除前一秒的十分之几。 默认值为 600 秒 （60 秒） 的十分之几秒。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 页超时不能为 0，由于固有的延迟。 页超时不能早于固有的延迟，即使页面超时选项设置为低于该值。|若要动态设置此选项，请使用**PAGETIMEOUT**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|只读|指定数据库为只读的。|若要动态设置此选项，请使用**READONLY**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|选择目录|显示一个对话框，您可以在其中选择包含想要访问的文件的目录。<br /><br /> 定义数据源目录时指定最常用文件的目录位于。 ODBC 驱动程序使用此目录作为默认目录。 如果经常使用，请将其他文件复制到此目录。 或者，可以限定 SELECT 语句中使用的目录名称的文件名称：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，你可以通过使用指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。|若要动态设置此选项，请使用**DEFAULTDIR**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|选择网络目录|包含 Paradox 锁定数据库，因为它包含 Pdoxusrs.net 文件的目录的完整路径 (Paradox 4 中。*x*) 或 Paradox.net 文件 (Paradox 5 中。*x*)。 如果目录不包含这些文件之一，Paradox 驱动程序将创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 可以选择在网络目录之前，必须输入在 Paradox 用户名**用户名**文本框。 单击**选择网络目录**选择网络目录。|若要动态设置此选项，请使用**PARADOXNETPATH**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|用户名|Paradox 用户名称。 这是当遇到锁 Paradox 文件的其他用户显示的名称。|若要动态设置此选项，请使用**PARADOXUSERNAME**调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|
