---
title: 直接连接到驱动程序 |Microsoft 文档
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
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f85b319ec264f9784953f12f93100660db614cbb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-directly-to-drivers"></a>直接连接到驱动程序
中所述已[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)前面的本部分中，某些应用程序不希望在所有使用数据源。 相反，他们想要直接连接到驱动程序。 **SQLDriverConnect**为应用程序直接连接到驱动程序而无需指定数据源提供的方法。 从概念上讲，在运行时创建临时数据源。  
  
 若要直接连接到驱动程序，应用程序指定**驱动程序**而不是连接字符串中的关键字**DSN**关键字。 值**驱动程序**关键字是驱动程序的说明，以返回**SQLDrivers**。 例如，假设某个驱动程序具有说明 Paradox 驱动程序，并且需要包含数据文件的目录的名称。 若要连接到此驱动程序，应用程序可以使用任一以下连接字符串：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 与第一个字符串，该驱动程序不需要任何附加信息。 替换为第二个字符串，该驱动程序将需要提示输入包含数据文件的目录的名称。
