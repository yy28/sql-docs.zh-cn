---
title: 数据截断检测使用 ExtendedAnsiSQL 启用 |Microsoft 文档
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
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 070537a00c0d179888260bc5cdcdfac0540f12dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>启用使用 ExtendedAnsiSQL 数据截断检测
当 ExtendedAnsiSQL 标志已开启并应用程序将数据插入到 char 或二进制列数据被截断时，则将检测到截断。 当关闭 ExtendedAnsiSQL 标志时，数据截断而不发出警告，因为其在以前版本的 ODBC 桌面数据库驱动程序。
