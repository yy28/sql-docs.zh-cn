---
title: 默认 C 数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70964b9d2a438805194f9816473fdf81d0d39f3f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="default-c-data-types"></a>默认 C 数据类型
如果应用程序指定在 SQL_C_DEFAULT **SQLBindCol**， **SQLGetData**，或**SQLBindParameter**，驱动程序假定的 C 数据类型的输出或输入的缓冲区对应于 SQL 数据类型的列或缓冲区绑定到的参数。  
  
> [!IMPORTANT]  
>  可互操作的应用程序不应使用 SQL_C_DEFAULT。 相反，它们应始终指定他们使用的缓冲区的 C 类型。 这是因为驱动程序不能始终正确地确定的默认 C 类型，原因如下：  
  
-   如果 DBMS 提升 SQL 数据类型的列或参数时，该驱动程序无法确定列或参数的原始 SQL 数据类型。 因此，它无法确定相应的默认 C 数据类型。  
  
-   如果驱动程序无法确定是否已签名的特定列或参数，如通常是这种情况，在这种由 DBMS，驱动程序无法确定是否的相应默认 C 数据类型应是有符号或无符号。  
  
     因为 SQL_C_DEFAULT 是提供仅作为编程方便起见，应用程序不会丢失任何功能时它指定实际的 C 数据类型。  
  
 显示每个 SQL 数据类型的默认 C 数据类型的表包含在[转换数据从 SQL C 数据类型到](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)、 本附录内容更高版本。
