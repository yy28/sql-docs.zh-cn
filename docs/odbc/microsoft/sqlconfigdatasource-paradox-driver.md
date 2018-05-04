---
title: SQLConfigDataSource （Paradox 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ce62252364cc9367d1335dbe82e721612517c70
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource （Paradox 驱动程序）
> [!NOTE]  
>  本主题提供 Paradox 特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序的序列。<br /><br /> 当使用 Paradox 驱动程序时，序列可以是 ASCII （默认值）、 国际、 瑞典语-芬兰语或挪威语丹麦语。<br /><br /> 这将设置为相同的选项**排序规则序列**在安装程序对话框中。|  
|DBQ|数据库文件的名称。<br /><br /> 这将设置为相同的选项**数据库**在安装程序对话框中。|  
|DEFAULTDIR|所指定的路径的目录。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置为相同的选项**说明**在安装程序对话框中。|  
|DRIVER|到驱动程序 DLL 路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|独占|确定数据库是否将 （一次只能由一个用户访问） 以独占方式打开或共享模式 （通过多个用户一次）。 可以是 true （独占模式） 或 false （共享模式）。<br /><br /> 这将设置为相同的选项**独占**在安装程序对话框中。|  
|FIL|文件类型 Paradox 3.x，Paradox 4.x 或 Paradox 5.x|  
|文件类型|文本驱动程序 （文本） 的文件类型。|  
|PAGETIMEOUT|以十分之一第二个，页 （如果未使用） 在被删除之前保留在缓冲区中指定的时间，段。 默认值为 600 秒 （60 秒） 的十分之几。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**页超时**在安装程序对话框中。|  
|PARADOXNETPATH|包含 Paradox 锁定数据库，因为它包含 PDOXUSRS.net 文件的目录的完整路径 (在 Paradox 4。*x*) 或 PARADOX.net 文件 (在 Paradox 5。*x*)。 如果目录不包含这些文件之一，则可能是驱动程序将创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 可以选择网络目录之前，必须输入 Paradox 用户名称。<br /><br /> 这将设置为相同的选项**选择网络目录**在安装程序对话框中。|  
|PARADOXNETSTYLE|对于 Paradox 驱动程序，网络访问访问 Paradox 数据时要使用的样式： Paradox 3 任一"3.x"。*x*或"4.x"可能是 4。*x*或 5。*x*。 可以将设置为"3.x"或"4.x"中，如果版本为 Paradox 4。*x*或 5。*x*; 如果版本为 Paradox 3。*x*的样式必须是"3.x"。<br /><br /> 这将设置为相同的选项**Net 样式**在安装程序对话框中。|  
|PARADOXUSERNAME|对于 Paradox 驱动程序，可能是用户名称。<br /><br /> 这将设置为相同的选项**用户名**在安装程序对话框中。|  
|PWD|密码。<br /><br /> 这是一个可选的关键字，将永远不会写入到文件由驱动程序。 对的调用中使用**SQLDriverConnect**针对密码保护 Paradox 文件。 每次打开表，所用的密码才有效。 如果没有密码传递连接字符串中，为该表不建立任何密码。 如果表具有不同的密码，多个不在同一会话中中, 打开，也可以将表联接。|  
|READONLY|若要使文件成为只读的;如果为 FALSE，以使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**在安装程序对话框中。|  
|线程|要使用的引擎的后台线程数。 此值为 3，并且不能更改。<br /><br /> 这将设置为相同的选项**线程**在安装程序对话框中。|
