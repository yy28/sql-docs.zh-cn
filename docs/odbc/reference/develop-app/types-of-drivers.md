---
title: 类型的驱动程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea99ec6a5b0a76ce0647e3681a4cf919d3f086b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087767"
---
# <a name="types-of-drivers"></a>驱动程序类型
ODBC 驱动程序可以进行分类，如下所示：  
  
-   **32 位 ODBC 2。**  
     **_x_驱动程序**的 32 位驱动程序的：  
  
    -   导出仅 ODBC *2.x*函数。  
  
    -   表现出 ODBC *2.x*行为的更改的行为。  
  
-   **ISO 和打开组兼容的驱动程序**的 32 位驱动程序的：  
  
    -   将导出的 Open Group 或 ISO CLI 文档中所述的所有函数。 这将在 ODBC 中包括一些不推荐使用的函数。  
  
    -   出现 ODBC 3.0 现象行为的更改。  
  
    -   不一定会通过 ODBC 3.0 驱动程序管理器。  
  
-   **ODBC 3.0 驱动程序**的 32 位驱动程序的：  
  
    -   导出仅作用减去 ODBC 3.0 中的过时的函数。  
  
    -   能够暴露 ODBC *2.x*行为或与行为的变化，有关 ODBC 3.0 行为基于 SQL_ATTR_APP_ODBC_VERSION 环境属性。  
  
-   **ODBC 3.5 （或更高版本） 的 ANSI 驱动程序**的 32 位驱动程序的：  
  
    -   导出仅作用中减去的 ODBC 3.5 过时的函数。  
  
    -   能够暴露 ODBC *2.x*行为或 ODBC 3.0 的行为或与行为的变化，有关 ODBC 3.5 行为基于 SQL_ATTR_APP_ODBC_VERSION 环境属性。  
  
-   **ODBC 3.5 （或更高版本） 的 Unicode 驱动程序**的 32 位驱动程序的：  
  
    -   支持 ODBC 3.5 ANSI 驱动程序的所有功能。  
  
    -   将导出所有 ODBC 字符串 Api 的 Unicode 版本。  
  
    -   可以存储和处理数据源上的 Unicode 数据。  
  
> [!NOTE]  
>  16 位 ODBC 驱动程序不会直接使用 ODBC *3.x*驱动程序管理器。 但是，有 16 位驱动程序以使用 2.0 ODBC 驱动程序管理器，它随后 thunk 最多可能*3.x*驱动程序管理器。
