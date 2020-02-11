---
title: SQLGetData （桌面数据库驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 086c5381f1801baf919508525c17faab93746ca0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003356"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData（桌面数据库驱动程序）
无论列是否有绑定列，此函数都可以从任何列中检索数据，而不考虑检索列的顺序。  
  
> [!NOTE]  
>  \*在 Jet 4.0 数据库上绑定到超过510个字符的 ANSI 数据时， **SQLGetData**中的 pcbValue 可能会返回实际可用字符数的两倍。 大于或等于510的字符值将返回实际的 cbValue。
