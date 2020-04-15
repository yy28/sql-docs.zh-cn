---
title: SQLGet数据（桌面数据库驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304118"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData（桌面数据库驱动程序）
此函数可以从任何列检索数据，无论列之后是否有绑定列，也不管检索列的顺序如何。  
  
> [!NOTE]  
>  \*在 Jet 4.0 数据库中绑定到 ANSI 数据时 **，SQLGetData**中的 pcbValue 返回的字符数可能是实际可用的字符数的两倍。 510 或更少的字符值将返回实际 cbValue。
