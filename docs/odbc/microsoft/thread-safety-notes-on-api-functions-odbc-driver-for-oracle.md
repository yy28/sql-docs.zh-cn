---
title: 线程安全性注意事项 API 函数 （Oracle ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d1faa7dfd8873b8c11cda5cb3e67d5408c35474
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633212"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函数线程安全性注意事项（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Microsoft ODBC Driver for Oracle 是线程安全的。但是，Oracle 不允许在单个连接上多个并发的语句。 该驱动程序强制实施此限制。 换而言之，在多线程应用程序，尽管任何线程能调入 Oracle ODBC 驱动程序在任何时候，该驱动程序阻止从同一连接上的驱动程序的其他任何线程直到原始线程会使该驱动程序。  
  
 如果有两个不同的连接上的两个语句，该驱动程序不会阻止。 但是，如果没有与两个语句的单个连接，可能会阻塞。
