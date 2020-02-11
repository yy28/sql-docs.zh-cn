---
title: 驱动程序的类型 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087767"
---
# <a name="types-of-drivers"></a>驱动程序类型
ODBC 驱动程序可以按如下方式分类：  
  
-   **32位 ODBC 2。**  
     ** _x_驱动程序**A 32 位驱动程序：  
  
    -   仅*导出 ODBC 2.x 函数。*  
  
    -   展示行为*更改的 ODBC 2.x*行为。  
  
-   **ISO 并打开与组兼容的驱动程序**一个32位驱动程序，该驱动程序：  
  
    -   导出打开组或 ISO CLI 文档中记录的所有函数。 这将包括 ODBC 中弃用的一些函数。  
  
    -   展示行为更改的 ODBC 3.0 行为。  
  
    -   不一定要经过 ODBC 3.0 驱动程序管理器。  
  
-   **ODBC 3.0 驱动程序**一个32位驱动程序，该驱动程序：  
  
    -   仅导出 ODBC 3.0 中不推荐使用的函数的函数。  
  
    -   基于 SQL_ATTR_APP_ODBC_VERSION 环境属性，能够使 ODBC 2.x 行为或 ODBC *3.0 行为与*行为更改相关。  
  
-   **ODBC 3.5 （或更高版本） ANSI 驱动程序**一个32位驱动程序，该驱动程序：  
  
    -   仅导出 ODBC 3.5 中不推荐使用的函数的函数。  
  
    -   基于 SQL_ATTR_APP_ODBC_VERSION 环境属性，能够使 ODBC 2.x 行为或 ODBC *3.0 行为或*odbc 3.5 行为与行为更改相关。  
  
-   **ODBC 3.5 （或更高版本） Unicode 驱动程序**一个32位驱动程序，该驱动程序：  
  
    -   支持 ODBC 3.5 ANSI 驱动程序的所有功能。  
  
    -   导出所有 ODBC 字符串 Api 的 Unicode 版本。  
  
    -   可以存储和处理数据源上的 Unicode 数据。  
  
> [!NOTE]  
>  16位 ODBC 驱动程序不会直接*使用 odbc 1.X*驱动程序管理器。 但是，16位驱动程序可以与 2.0 ODBC 驱动程序管理器配合使用，后者随后会成为1.x 驱动程序管理*器。*
