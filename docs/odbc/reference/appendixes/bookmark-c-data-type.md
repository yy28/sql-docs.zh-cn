---
title: 书签 C 数据类型 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 566f1065d30a47b2db234ba1f11f877725189fb7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292287"
---
# <a name="bookmark-c-data-type"></a>书签 C 数据类型
书签 C 数据类型允许应用程序检索书签。 书签 C 类型仅用于检索长度可可变的书签值;它们不应转换为其他数据类型。 应用程序**从结果集**的第 0 列检索书签（操作为 SQL_ADD）、SQLFetch、SQLFetchScroll 或**SQLFetch****SQLGetData**。 **SQLFetchScroll** 有关详细信息，请参阅[书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出了书签 C 数据类型的*CType*值、实现书签 C 数据类型的 ODBC C 数据类型以及 SQL 中此数据类型的定义。H。  
  
> [!NOTE]
>  已弃用SQL_C_BOOKMARK数据类型。 ODBC *3.x*应用程序不应使用SQL_C_BOOKMARK。 ODBC *3.x*驱动程序只有在希望使用 ODBC *2.x*应用程序时才需要支持SQL_C_BOOKMARK。 当应用程序使用 ODBC *2.x*驱动程序工作时，驱动程序管理器将SQL_C_VARBOOKMARK映射到SQL_C_BOOKMARK。  
  
|C 类型标识符|ODBC C 型定义|C 类型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />（不推荐使用）|书签|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR ||unsigned char *|
