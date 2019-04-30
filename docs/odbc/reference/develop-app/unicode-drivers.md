---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e555ff4a3b33c4c827371dc1ad63546736d7189
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473038"
---
# <a name="unicode-drivers"></a>Unicode 驱动程序
驱动程序是否应为 Unicode 或 ANSI 驱动程序完全取决于数据源的特性。 如果数据源支持 Unicode 数据，该驱动程序应为 Unicode 驱动程序。 如果数据源仅支持 ANSI 数据，该驱动程序应保持 ANSI 驱动程序。  
  
 Unicode 驱动程序必须导出**SQLConnectW**识别为 Unicode 驱动程序由驱动程序管理器。  
  
 Unicode 驱动程序必须接受 Unicode 函数 (带有后缀*W*) 和存储 Unicode 数据。 它还可以接受 ANSI 函数，但不需要。 (驱动程序管理器将使用的 ANSI 函数调用不传递*A*后缀驱动程序，但将它为 ANSI 函数调用中的，而后缀，然后将它放到驱动程序。)  
  
 Unicode 驱动程序必须能够返回 Unicode 或 ANSI，在结果集，具体取决于应用程序的绑定。 如果应用程序绑定到 SQL_C_CHAR，Unicode 驱动程序必须将 SQL_WCHAR 数据转换为 SQL_CHAR。 驱动程序管理器将映射 SQL_C_WCHAR SQL_C_CHAR 到 ANSI 的驱动程序但没有 Unicode 驱动程序的映射。  
  
> [!NOTE]  
>  在确定驱动程序类型，驱动程序管理器将调用**SQLSetConnectAttr**并将 SQL_ATTR_ANSI_APP 属性设置在连接时。 如果应用程序使用的 ANSI Api，SQL_ATTR_ANSI_APP 将设置为 SQL_AA_TRUE，和如果它使用 Unicode，它将设置为 SQL_AA_FALSE 的值。 使用此属性，以便该驱动程序可能会表现出不同的行为根据应用程序类型。 该属性不能直接，由应用程序设置和不受**SQLGetConnectAttr**。 如果驱动程序的行为的 ANSI 和 Unicode 应用程序，它应为此属性返回 SQL_ERROR。 如果该驱动程序返回 SQL_SUCCESS，驱动程序管理器将使用连接池时分离 ANSI 和 Unicode 的连接。
