---
title: Unicode 驱动程序 |微软文档
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
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284349"
---
# <a name="unicode-drivers"></a>Unicode 驱动程序
驱动程序是 Unicode 驱动程序还是 ANSI 驱动程序完全取决于数据源的性质。 如果数据源支持 Unicode 数据，则驱动程序应为 Unicode 驱动程序。 如果数据源仅支持 ANSI 数据，则驱动程序应仍为 ANSI 驱动程序。  
  
 Unicode 驱动程序必须导出**SQLConnectW**才能被驱动程序管理器识别为 Unicode 驱动程序。  
  
 Unicode 驱动程序必须接受 Unicode 函数（后缀为*W）* 并存储 Unicode 数据。 它也可以接受 ANSI 函数，但不是必需的。 （驱动程序管理器不会将带有*A*后缀的 ANSI 函数调用传递给驱动程序，而是将其转换为没有后缀的 ANSI 函数调用，然后将其传递给驱动程序。  
  
 Unicode 驱动程序必须能够返回 Unicode 或 ANSI 中的结果集，具体取决于应用程序的绑定。 如果应用程序绑定到SQL_C_CHAR，Unicode 驱动程序必须将SQL_WCHAR数据转换为SQL_CHAR。 驱动程序管理器将SQL_C_WCHAR映射到 ANSI 驱动程序SQL_C_CHAR，但不映射 Unicode 驱动程序。  
  
> [!NOTE]  
>  确定驱动程序类型时，驱动程序管理器将调用**SQLSetConnectAttr**并在连接时设置SQL_ATTR_ANSI_APP属性。 如果应用程序使用 ANSI API，SQL_ATTR_ANSI_APP将设置为SQL_AA_TRUE，如果应用程序使用 Unicode，则它将设置为SQL_AA_FALSE的值。 使用此属性，以便驱动程序可以基于应用程序类型显示不同的行为。 该属性不能由应用程序直接设置，并且**SQLGetConnectAttr**不支持该属性。 如果驱动程序对 ANSI 和 Unicode 应用程序都表现出相同的行为，则应返回此属性SQL_ERROR。 如果驱动程序返回SQL_SUCCESS，则驱动程序管理器将在使用连接池时分离 ANSI 和 Unicode 连接。
