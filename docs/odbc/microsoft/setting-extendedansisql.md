---
title: 设置 ExtendedAnsiSQL |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c120d665c1b3c1838214a8991334d421b96c71ab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="setting-extendedansisql"></a>设置 ExtendedAnsiSQL
该属性可通过添加 ExtendedAnsiSQL 属性控制的连接字符串：  
  
|“值”|Description|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 （默认值）|此设置不启用新功能。|  
|ExtendedAnsiSQL = 1|此设置启用了新功能。|  
  
 该属性也可以在通过 DSN 设置**高级选项**对话框中配置通过控制面板的 DSN 时。  
  
 将属性设置为 0 将禁用新的功能;将其设置为 1 启用了新功能。  
  
 此外可以使用 SQLSetConnectAttr() 设置该属性。 属性值为 65501，并设置为 SQLINTEGER 值为 1 或 0，如前面的表中所述。 则可以调用它之前或之后连接，但它是更好的做法由于在其中的驱动程序进程缓存连接属性和连接字符串的顺序连接后调用它。
