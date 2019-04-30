---
title: 默认 C 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c4147b1bfa5ffb1e379c3aa8be2c9ea2a9d2775
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240971"
---
# <a name="default-c-data-types"></a>默认 C 数据类型
如果应用程序指定中的 SQL_C_DEFAULT **SQLBindCol**， **SQLGetData**，或**SQLBindParameter**，驱动程序假定的 C 数据类型的输出或输入的缓冲区对应于 SQL 数据类型的参数缓冲区绑定到的列。  
  
> [!IMPORTANT]  
>  可互操作应用程序不应使用 SQL_C_DEFAULT。 相反，它们应始终指定他们所使用的缓冲区的 C 类型。 这是因为驱动程序不能始终正确确定的默认 C 类型，原因如下：  
  
-   如果 DBMS 提升 SQL 数据类型的列或参数时，该驱动程序无法确定列或参数的原始 SQL 数据类型。 因此，它无法确定相应的默认 C 数据类型。  
  
-   如果驱动程序无法确定是否已签名的特定列或参数，如通常是这种情况，在这种处理 DBMS 的驱动程序无法确定相应的默认 C 数据类型是否应签名或未签名。  
  
     SQL_C_DEFAULT 提供只是为了编程方便，因为该应用程序不会不会丢失任何功能，它指定实际的 C 数据类型时。  
  
 中包含一个显示每个 SQL 数据类型的默认 C 数据类型表[从 SQL 到 C 数据类型的转换的数据](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)、 本附录中更高版本。
