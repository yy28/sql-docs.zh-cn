---
title: 驱动程序类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de6d8e1473f127d28c69969e0fc298afd69d3023
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304868"
---
# <a name="types-of-drivers"></a>驱动程序类型
ODBC 驱动程序可以分类如下：  
  
-   **32 位 ODBC 2。**  
     ** _x_驱动程序**32 位驱动程序， ：  
  
    -   仅导出 ODBC *2.x*功能。  
  
    -   展示 ODBC *2.x*行为变化的行为。  
  
-   **ISO 和打开组兼容驱动程序**32 位驱动程序，  
  
    -   导出在开放组或 ISO CLI 文档中记录的所有功能。 这将包括一些在 ODBC 中弃用的功能。  
  
    -   展示 ODBC 3.0 行为更改的行为。  
  
    -   不一定通过 ODBC 3.0 驱动程序管理器。  
  
-   **ODBC 3.0 驱动程序**32 位驱动程序，  
  
    -   仅导出 ODBC 3.0 减去弃用函数中的函数。  
  
    -   能够根据SQL_ATTR_APP_ODBC_VERSION环境属性，在行为变化方面展示 ODBC *2.x*行为或 ODBC 3.0 行为。  
  
-   **ODBC 3.5（或更高版本）ANSI 驱动程序**32 位驱动程序，  
  
    -   仅导出 ODBC 3.5 减去弃用函数中的函数。  
  
    -   能够根据SQL_ATTR_APP_ODBC_VERSION环境属性，展示ODBC *2.x*行为或ODBC 3.0行为，或ODBC 3.5行为行为。  
  
-   **ODBC 3.5（或更高版本）统一代码驱动程序**32 位驱动程序，  
  
    -   支持 ODBC 3.5 ANSI 驱动程序的所有功能。  
  
    -   导出所有 ODBC 字符串 API 的 Unicode 版本。  
  
    -   可以在数据源上存储和处理 Unicode 数据。  
  
> [!NOTE]  
>  16 位 ODBC 驱动程序不会直接与 ODBC *3.x*驱动程序管理器配合使用。 但是，16 位驱动程序可以使用 2.0 ODBC 驱动程序管理器，该管理器随后会连接到*3.x*驱动程序管理器。
