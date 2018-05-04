---
title: 以编程方式为 Paradox 驱动程序设置选项 |Microsoft 文档
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
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fa8084499f38a7152eb5eeab50010b919f4a06e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以编程方式为 Paradox 驱动程序的的设置选项
|选项|Description|方法|  
|------------|-----------------|------------|  
|目录|设置的目标的目录。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|排序规则序列|字段的排序顺序的序列。<br /><br /> 序列可以是 ASCII （默认值）、 国际、 瑞典语-芬兰语或挪威语丹麦语。|若要动态设置此选项，使用**COLLATINGSEQUENCE**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Description|数据源; 中的数据的可选描述例如，"雇用日期、 薪金历史记录和当前查看的所有雇员。"|若要动态设置此选项，使用**说明**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|排他|如果**独占**框为选中状态，数据库将以独占方式打开并将一次只能有一个用户可以访问。 以独占模式运行时，为提高性能。|若要动态设置此选项，使用**独占**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Net 样式|要访问 Paradox 数据时使用的网络访问样式： 任一"3。*x*"Paradox 3。*x*或"4。*x*"可能是 4。*x*或 5。*x*。 可以将设置为"3。*x*"或"4。*x*"如果版本为可能是 4。*x*或 5。*x*; 如果版本为 Paradox 3。*x*的样式必须是"3。*x*"。|若要动态设置此选项，使用**PARADOXNETSTYLE**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|页超时|以十分之一第二个，页 （如果未使用） 在被删除之前保留在缓冲区中指定的时间，段。 默认值为 600 秒 （60 秒） 的十分之几。 此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 页超时不能为 0，由于固有的延迟。 页超时不能早于固有的延迟，即使页 timeout 选项设置为低于该值的过程。|若要动态设置此选项，使用**PAGETIMEOUT**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|只读|将数据库指定为只读的。|若要动态设置此选项，使用**READONLY**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|选择目录|显示一个对话框，你可以在其中选择包含你想要访问的文件的目录。<br /><br /> 介绍了当定义数据源目录指定你最常用文件的目录。 ODBC 驱动程序使用此目录作为默认目录。 将其他文件复制到此目录中，如果经常使用它们。 或者，可以限定在 SELECT 语句以目录名称的文件名称：<br /><br /> 选择\*从 C:\MYDIR\EMP<br /><br /> 或者，你可以通过指定新的默认目录**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 选项的函数。|若要动态设置此选项，使用**DEFAULTDIR**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|选择网络目录|包含 Paradox 锁定数据库，因为它包含 Pdoxusrs.net 文件的目录的完整路径 (在 Paradox 4。*x*) 或 Paradox.net 文件 (在 Paradox 5。*x*)。 如果目录不包含这些文件之一，则可能是驱动程序将创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 你可以选择网络目录之前，你必须输入你 Paradox 的用户名中**用户名**文本框。 单击**选择网络目录**选择网络目录。|若要动态设置此选项，使用**PARADOXNETPATH**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|用户名|Paradox 用户名称。 这是一遇到锁时向 Paradox 文件的其他用户显示的名称。|若要动态设置此选项，使用**PARADOXUSERNAME**对的调用中的关键字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|
