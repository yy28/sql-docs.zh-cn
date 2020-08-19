---
description: API 函数线程安全性注意事项（Oracle ODBC 驱动程序）
title: 线程安全说明 (用于 Oracle) 的 ODBC 驱动程序的 API 函数 |Microsoft Docs
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
ms.openlocfilehash: 8c7da346832e2682caa02bdbdae91a1133a9cbaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449079"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>API 函数线程安全性注意事项（Oracle ODBC 驱动程序）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 适用于 Oracle 的 Microsoft ODBC 驱动程序是线程安全的;但是，Oracle 不允许单个连接使用多个并发语句。 驱动程序强制实施此限制。 换句话说，在多线程应用程序中，尽管任何线程可以随时调入到 Oracle 的 ODBC 驱动程序，但是，驱动程序会阻止来自同一连接上的驱动程序的任何其他线程，直到原始线程退出该驱动程序。  
  
 如果两个不同的连接上有两个语句，驱动程序不会被阻止。 但是，如果有一个与两个语句的连接，则可能会发生阻塞。
