---
title: SQLConfig数据源（悖论驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283927"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供特定于悖论驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLConfigDataSource**函数用于动态添加、修改或删除数据源，使用以下关键字。  
  
|关键字|描述|  
|-------------|-----------------|  
|整理顺序|字段排序的顺序。<br /><br /> 使用 Paradox 驱动程序时，序列可以是 ASCII（默认）、国际、瑞典-芬兰或挪威-丹麦。<br /><br /> 这将设置与设置对话框中 **"整理序列"** 相同的选项。|  
|DBQ|数据库文件的名称。<br /><br /> 这将在设置对话框中设置与**数据库**相同的选项。|  
|默认DIR|目录的路径规范。|  
|DESCRIPTION|数据源中数据的说明。<br /><br /> 这将设置与设置对话框中的 **"说明"** 相同的选项。|  
|DRIVER|驱动程序 DLL 的路径规范。|  
|驱动程序 ID|驱动程序的整数 ID。<br /><br /> 26 （悖论 3.x）<br /><br /> 282 （悖论 4.x）<br /><br /> 538 （悖论 5.x）|  
|独家|确定数据库将以独占模式打开（一次只由一个用户访问）还是共享模式（一次由多个用户访问）。 可以是 true（独占模式）或 false（共享模式）。<br /><br /> 这将在设置对话框中设置与 **"独占"** 相同的选项。|  
|FIL|文件类型悖论 3.x、悖论 4.x 或悖论 5.x|  
|文件类型|文本驱动程序（文本）的文件类型。|  
|页面超时|指定页面（如果不使用）在删除之前保留在缓冲区中的时间段（以十分之一秒表示）。 默认值为 600 秒（60 秒）。 请注意，此选项适用于使用 ODBC 驱动程序的所有数据源。<br /><br /> 这将在设置对话框中设置与**页面超时**相同的选项。|  
|悖论网络路径|包含 Paradox 锁数据库的目录的完整路径，因为它包含PDOXUSRS.net文件（在悖论 4 中）。*x*） 或PARADOX.net文件（在悖论 5 中）。*x*）。 如果目录不包含这些文件之一，则 Paradox 驱动程序将创建一个。 有关这些文件的信息，请参阅 Paradox 文档。<br /><br /> 在选择网络目录之前，必须输入 Paradox 用户名。<br /><br /> 这将在设置对话框中设置与**选择网络目录**相同的选项。|  
|悖论网络风格|对于悖论驱动程序，在访问悖论数据时要使用的网络访问样式：对于悖论 3 的"3.x"。*x*或"4.x"表示悖论 4。*x*或 5。*x*. . 如果版本为悖论 4，则可以设置为"3.x"或"4.x"。*x*或 5。*x;* 如果版本是悖论 3。*x*，样式必须为"3.x"。<br /><br /> 这将在设置对话框中设置与 **"网络样式"** 相同的选项。|  
|悖论|对于悖论驱动程序，悖论用户名。<br /><br /> 这将在设置对话框中设置与**用户名**相同的选项。|  
|PWD|密码。<br /><br /> 这是一个可选的关键字，驱动程序永远不会写入文件。 它用于针对密码安全的悖论文件的调用**SQLDriverConnect。** 每当打开表时，使用的密码将有效。 如果在连接字符串中未传递密码，则未为该表建立密码。 如果表具有不同的密码，则无法在同一会话中打开多个密码，也无法联接表。|  
|READONLY|TRUE 使文件为只读;FALSE 使文件不只读。<br /><br /> 这将在设置对话框中设置与 **"只读"** 相同的选项。|  
|线程|发动机要使用的后台线程数。 此值为 3，无法更改。<br /><br /> 这将设置与设置对话框中的 **"线程"** 相同的选项。|
