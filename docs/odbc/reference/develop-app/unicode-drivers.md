---
description: Unicode 驱动程序
title: Unicode 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1acdb0c630fe5f4b1b22f51015e7ee94e7d8a56a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424479"
---
# <a name="unicode-drivers"></a>Unicode 驱动程序
驱动程序是 Unicode 驱动程序还是 ANSI 驱动程序完全取决于数据源的性质。 如果数据源支持 Unicode 数据，则驱动程序应为 Unicode 驱动程序。 如果数据源仅支持 ANSI 数据，则驱动程序应仍为 ANSI 驱动程序。  
  
 Unicode 驱动程序必须将 **SQLConnectW** 导出为由驱动程序管理器识别为 Unicode 驱动程序。  
  
 Unicode 驱动程序必须接受 (带有 *W* 后缀的 unicode 函数) 并存储 Unicode 数据。 它还可以接受 ANSI 函数，但并不是必需的。  (驱动程序管理器不会向驱动程序传递带有后缀 *的* ansi 函数调用，但会将其转换为不带后缀的 ansi 函数调用，然后将其传递给驱动程序。 )   
  
 Unicode 驱动程序必须能够返回 Unicode 或 ANSI 中的结果集，具体取决于应用程序的绑定。 如果应用程序绑定到 SQL_C_CHAR，则 Unicode 驱动程序必须将 SQL_WCHAR 数据转换为 SQL_CHAR。 驱动程序管理器会将 ANSI 驱动程序的 SQL_C_WCHAR 映射到 SQL_C_CHAR，但不会映射 Unicode 驱动程序。  
  
> [!NOTE]  
>  确定驱动程序类型时，驱动程序管理器将调用 **SQLSetConnectAttr** 并在连接时设置 SQL_ATTR_ANSI_APP 特性。 如果应用程序使用的是 ANSI Api，SQL_ATTR_ANSI_APP 将设置为 SQL_AA_TRUE，如果使用的是 Unicode，则会将其设置为 SQL_AA_FALSE 值。 使用此属性，以便驱动程序可以根据应用程序类型展示不同的行为。 此属性不能由应用程序直接设置，并且 **SQLGetConnectAttr**不支持该属性。 如果驱动程序的 ANSI 和 Unicode 应用程序的行为相同，则它应返回此属性 SQL_ERROR。 如果驱动程序返回 SQL_SUCCESS，则在使用连接池时，驱动程序管理器会将 ANSI 和 Unicode 连接隔开。
