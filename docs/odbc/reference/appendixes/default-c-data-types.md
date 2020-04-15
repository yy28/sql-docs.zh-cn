---
title: 默认 C 数据类型 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307048"
---
# <a name="default-c-data-types"></a>默认 C 数据类型
如果应用程序在**SQLBindCol、SQLGetData**或**SQLBind参数**中指定SQL_C_DEFAULT ，则驱动程序假定输出或输入缓冲区的 C 数据类型对应于缓冲区绑定到的列或参数的 SQL 数据类型。 **SQLGetData**  
  
> [!IMPORTANT]  
>  可互操作的应用程序不应使用SQL_C_DEFAULT。 相反，它们应始终指定他们正在使用的缓冲区的 C 类型。 这是因为驱动程序无法始终正确确定默认 C 类型，原因如下：  
  
-   如果 DBMS 升级列或参数的 SQL 数据类型，则驱动程序无法确定列或参数的原始 SQL 数据类型。 因此，它无法确定相应的默认 C 数据类型。  
  
-   如果驱动程序无法确定是否对特定列或参数进行签名（DBMS 处理时通常的情况）驱动程序无法确定应签名还是未签名相应的默认 C 数据类型。  
  
     由于SQL_C_DEFAULT仅为编程方便而提供，因此当应用程序指定实际 C 数据类型时，不会丢失任何功能。  
  
 在本附录的后面部分，显示每个 SQL 数据类型的默认 C 数据类型的表包含在[将数据从 SQL 转换为 C 数据类型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中。
