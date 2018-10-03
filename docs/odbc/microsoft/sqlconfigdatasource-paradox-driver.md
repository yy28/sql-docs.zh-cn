---
title: SQLConfigDataSource （Paradox 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad9c944af33da86e0d4f85769288f4ab7b6c369f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694586"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Paradox 驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLConfigDataSource**函数，用于添加、 修改或删除数据源动态使用下列关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序的序列。<br /><br /> 该规则使用 Paradox 驱动程序时，可以是 ASCII （默认值）、 国际、 瑞典语-芬兰语或挪威语-丹麦语。<br /><br /> 这将设置为相同的选项**排序规则序列**中设置的对话框。|  
|DBQ|数据库文件的名称。<br /><br /> 这将设置为相同的选项**数据库**中设置的对话框。|  
|DEFAULTDIR|所指定的路径的目录。|  
|DESCRIPTION|数据源中的数据说明。<br /><br /> 这将设置为相同的选项**说明**中设置的对话框。|  
|DRIVER|路径规范，以驱动程序 DLL。|  
|DRIVERID|驱动程序的一个整数 ID。<br /><br /> 26 (paradox 3.x)<br /><br /> 282 (paradox 4.x)<br /><br /> 538 (paradox 5.x)|  
|排他|确定数据库是否将排他模式 （一次只能由一个用户访问） 中打开或共享模式 （一次通过多个用户访问）。 可以是 true （排他模式） 或 false （共享模式）。<br /><br /> 这将设置为相同的选项**独占**中设置的对话框。|  
|FIL|文件类型 Paradox 3.x，Paradox 4.x 或 Paradox 5.x|  
|文件类型|文本驱动程序 （文本） 的文件类型。|  
|PAGETIMEOUT|指定时间，的段中 （如果不使用） 会保留一页在缓冲区中被删除前一秒的十分之几。 默认值为 600 秒 （60 秒） 的十分之几秒。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将设置为相同的选项**页超时**中设置的对话框。|  
|PARADOXNETPATH|包含 Paradox 锁定数据库，因为它包含 PDOXUSRS.net 文件的目录的完整路径 (Paradox 4 中。*x*) 或 PARADOX.net 文件 (Paradox 5 中。*x*)。 如果目录不包含这些文件之一，Paradox 驱动程序将创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 可以选择在网络目录之前，必须输入 Paradox 用户名称。<br /><br /> 这将设置为相同的选项**选择网络目录**中设置的对话框。|  
|PARADOXNETSTYLE|Paradox 驱动程序的网络访问的访问 Paradox 数据时要使用的样式： Paradox 3 任一"3.x"。*x*或"4.x"可能是 4。*x*或 5。*x*。 可以将设置为"3.x"或"4.x"中，如果版本为 Paradox 4。*x*或 5。*x*; 如果版本为 Paradox 3。*x*，该样式必须是"3.x"。<br /><br /> 这将设置为相同的选项**Net 样式**中设置的对话框。|  
|PARADOXUSERNAME|对于 Paradox 驱动程序，可能是用户名称。<br /><br /> 这将设置为相同的选项**用户名**中设置的对话框。|  
|PWD|密码。<br /><br /> 这是一个可选的关键字，将永远不会写入到该文件由驱动程序。 对的调用中使用**SQLDriverConnect**针对密码保护 Paradox 文件。 每次打开表，所用的密码会在有效。 如果没有密码的连接字符串中传递，该表的建立无密码。 如果表具有不同的密码，也不能在同一会话中打开多个不可以联接这些表。|  
|READONLY|若要使文件只读的;如果为 FALSE，则若要使文件不是只读的。<br /><br /> 这将设置为相同的选项**Read Only**中设置的对话框。|  
|线程|要使用的引擎的后台线程数。 此值为 3，而不能更改。<br /><br /> 这将设置为相同的选项**线程**中设置的对话框。|
