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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68e60d7ca9c37865c1b265297d24591638a44965
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283927"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 用于动态添加、修改或删除数据源的**SQLConfigDataSource**函数使用以下关键字。  
  
|关键字|说明|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|字段的排序顺序。<br /><br /> 使用 Paradox 驱动程序时，序列可以是 ASCII （默认值）、国际、瑞典语或挪威语-丹麦语。<br /><br /> 这会在 "安装程序" 对话框中设置与**排序顺序**相同的选项。|  
|DBQ|数据库文件的名称。<br /><br /> 这会在 "设置" 对话框中设置与**数据库**相同的选项。|  
|DEFAULTDIR|目录的路径规范。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这会在 "设置" 对话框中设置与 "**描述**" 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|DRIVERID|驱动程序的整数 ID。<br /><br /> 26（Paradox 1.x）<br /><br /> 282（Paradox 4.x）<br /><br /> 538（Paradox 为1.x）|  
|异|确定是以独占模式（一次只能由一个用户访问）还是共享模式（一次由多个用户访问）打开数据库。 可以为 true （独占模式）或 false （共享模式）。<br /><br /> 这会在 "设置" 对话框中设置与 "**独占**" 选项相同的选项。|  
|FIL|文件类型 Paradox 为1.x，Paradox 为6.x，或 Paradox 为6。x|  
|FILETYPE|文本驱动程序的文件类型（文本）。|  
|PAGETIMEOUT|指定在删除之前页（如果未使用）保留在缓冲区中的时间段（以十分之一为一秒）。 默认值为600，即十分之一秒（60秒）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这会设置与 "设置" 对话框中**页面超时**相同的选项。|  
|PARADOXNETPATH|包含 Paradox lock 数据库的目录的完整路径，因为它包含 PDOXUSRS.net 文件（在 Paradox 4 中）。*x*）或 PARADOX.net 文件（在 PARADOX 5 中。*x*）。 如果目录不包含这些文件中的一个，则 Paradox 驱动程序会创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 必须先输入 Paradox 用户名，然后才能选择网络目录。<br /><br /> 这会设置与 "设置" 对话框中的 "**选择网络目录**" 相同的选项。|  
|PARADOXNETSTYLE|对于 Paradox 驱动程序，要在访问 Paradox 数据时使用的网络访问样式： "3. x" 表示 Paradox 3。对于 Paradox 4，则为*x*或 "4.x"。*x*或5。*x*。 如果版本为 Paradox 4，则可以设置为 "3.x" 或 "4.x"。*x*或5。*x*;如果版本为 "Paradox 3"。*x*，样式必须是 "2.x"。<br /><br /> 这会在 "设置" 对话框中设置与**Net Style**相同的选项。|  
|PARADOXUSERNAME|对于 Paradox 驱动程序，Paradox 用户名。<br /><br /> 这会设置与 "设置" 对话框中的 "**用户名**" 相同的选项。|  
|PWD|密码。<br /><br /> 这是一个可选关键字，驱动程序永远不会将其写入文件中。 它用于针对密码保护的 Paradox 文件调用**SQLDriverConnect** 。 每次打开表时，所使用的密码都是有效的。 如果在连接字符串中未传递任何密码，则不会为该表建立密码。 如果表具有不同的密码，则无法在同一会话中打开多个表，也不能联接这些表。|  
|READONLY|若要使文件为只读，则为 TRUE;如果设置为 FALSE，则使文件不为只读。<br /><br /> 这会在 "设置" 对话框中设置与 "**只读**" 相同的选项。|  
|线程|引擎要使用的后台线程数。 此值为3，无法更改。<br /><br /> 这会设置与 "设置" 对话框中的**线程**相同的选项。|
