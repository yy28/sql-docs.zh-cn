---
title: 数据截断检测使用 ExtendedAnsiSQL 启用 |Microsoft 文档
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
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08183430384a7a5ced14871c7bd151cb21c40b2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32898342"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>启用使用 ExtendedAnsiSQL 数据截断检测
当 ExtendedAnsiSQL 标志已开启并应用程序将数据插入到 char 或二进制列数据被截断时，则将检测到截断。 当关闭 ExtendedAnsiSQL 标志时，数据截断而不发出警告，因为其在以前版本的 ODBC 桌面数据库驱动程序。
