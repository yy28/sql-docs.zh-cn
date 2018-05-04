---
title: 有关 API 函数 （适用于 Oracle 的 ODBC 驱动程序） 的线程安全性说明 |Microsoft 文档
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
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af91cf6ea125feaa814030c9eb462a096bbcd2e2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函数 （适用于 Oracle 的 ODBC 驱动程序） 的线程安全性注意事项
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Microsoft ODBC Driver for Oracle 是线程安全的;但是，Oracle 不允许在单个连接上多个并发的语句。 该驱动程序强制实施此限制。 换而言之，在多线程应用程序，尽管入适用于 Oracle ODBC 驱动程序中的任何线程可以调用任何时候，该驱动程序阻塞，从同一连接上的驱动程序的其他任何线程直到原始线程离开该驱动程序。  
  
 如果有两个不同的连接上的两个语句，该驱动程序不会阻止。 但是，如果没有与两个语句的单个连接，则潜在的阻塞。
