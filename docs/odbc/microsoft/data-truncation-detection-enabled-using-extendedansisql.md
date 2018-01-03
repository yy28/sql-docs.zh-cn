---
title: "数据截断检测使用 ExtendedAnsiSQL 启用 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f36a9de5b1ce9ca269511bb0a2a641d201ed37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>启用使用 ExtendedAnsiSQL 数据截断检测
当 ExtendedAnsiSQL 标志已开启并应用程序将数据插入到 char 或二进制列数据被截断时，则将检测到截断。 当关闭 ExtendedAnsiSQL 标志时，数据截断而不发出警告，因为其在以前版本的 ODBC 桌面数据库驱动程序。
