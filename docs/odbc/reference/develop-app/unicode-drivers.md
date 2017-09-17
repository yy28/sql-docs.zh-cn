---
title: "Unicode 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52afd6864229173b699df74410349b0cac482c98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="unicode-drivers"></a>Unicode 驱动程序
驱动程序是否应为 Unicode 驱动程序或 ANSI 驱动程序完全取决于数据源的特性。 如果数据源支持 Unicode 数据，该驱动程序应为 Unicode 驱动程序。 如果数据源仅支持 ANSI 数据，该驱动程序应保留 ANSI 驱动程序。  
  
 Unicode 驱动程序必须导出**SQLConnectW**识别为 Unicode 驱动程序的驱动程序管理器。  
  
 Unicode 驱动程序必须接受 Unicode 函数 (为后缀*W*) 和存储 Unicode 数据。 它还可以接受 ANSI 函数，但不要求。 (驱动程序管理器不能通过使用 ANSI 函数调用*A*后缀驱动程序，但将转换为 ANSI 它函数调用中的，而后缀，然后将其放到该驱动程序。)  
  
 Unicode 驱动程序必须能够在 Unicode 或 ANSI，返回结果集，具体取决于应用程序的绑定。 如果应用程序绑定到 SQL_C_CHAR，Unicode 驱动程序必须将 SQL_WCHAR 数据转换为 SQL_CHAR。 驱动程序管理器将映射 SQL_C_WCHAR 到 SQL_C_CHAR ANSI 驱动程序，但不不 Unicode 驱动程序的任何映射。  
  
> [!NOTE]  
>  驱动程序管理器在确定驱动程序类型时，将调用**SQLSetConnectAttr**并将 SQL_ATTR_ANSI_APP 属性设置在连接时。 SQL_ATTR_ANSI_APP 如果应用程序使用的 ANSI Api，将设置为 SQL_AA_TRUE，并且如果正在使用 Unicode，它将设置为 SQL_AA_FALSE 一个值。 使用此属性，以便该驱动程序会表现出不同的应用程序类型所基于的行为。 该属性不能直接，由应用程序设置和不支持通过**SQLGetConnectAttr**。 如果驱动程序的行为为 ANSI 和 Unicode 应用程序，则应为此属性返回 SQL_ERROR。 如果该驱动程序返回 SQL_SUCCESS，驱动程序管理器将使用连接池时分离 ANSI 和 Unicode 的连接。
