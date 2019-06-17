---
title: 直接连接到驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f5818d67659769ae104b3e98248c26f5b9fe8a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151243"
---
# <a name="connecting-directly-to-drivers"></a>直接连接到驱动程序
如已中所述[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)前面在本部分中，某些应用程序不希望在所有使用数据源。 相反，他们想要直接连接到驱动程序。 **SQLDriverConnect**为应用程序直接连接到驱动程序而无需指定数据源提供的方法。 从概念上讲，在运行时创建的临时数据源。  
  
 若要直接连接到驱动程序，该应用程序应指定**驱动程序**而不是在连接字符串中的关键字**DSN**关键字。 值**驱动程序**关键字与返回的驱动程序的说明**SQLDrivers**。 例如，假设驱动程序已说明 Paradox 驱动程序，并需要包含数据文件的目录的名称。 若要连接到此驱动程序，应用程序可以使用以下连接字符串之一：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 与第一个字符串，该驱动程序不需要任何其他信息。 使用第二个字符串，该驱动程序需要提示输入包含数据文件的目录的名称。
