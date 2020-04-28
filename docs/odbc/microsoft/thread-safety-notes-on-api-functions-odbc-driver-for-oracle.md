---
title: API 函数（Oracle ODBC 驱动程序）上的线程安全说明 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 489f0e99ea53d419ff94dddfeb22e37573abb874
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303068"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函数线程安全性注意事项（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 适用于 Oracle 的 Microsoft ODBC 驱动程序是线程安全的;但是，Oracle 不允许单个连接使用多个并发语句。 驱动程序强制实施此限制。 换句话说，在多线程应用程序中，尽管任何线程可以随时调入到 Oracle 的 ODBC 驱动程序，但是，驱动程序会阻止来自同一连接上的驱动程序的任何其他线程，直到原始线程退出该驱动程序。  
  
 如果两个不同的连接上有两个语句，驱动程序不会被阻止。 但是，如果有一个与两个语句的连接，则可能会发生阻塞。
