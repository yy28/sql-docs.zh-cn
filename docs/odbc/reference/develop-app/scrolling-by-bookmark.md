---
title: 按书签滚动 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 454e29abdf848fdf4f4eaae090e7cc326f0048df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304188"
---
# <a name="scrolling-by-bookmark"></a>按书签滚动
使用**SQLFetchScroll**提取行时，应用程序可以使用书签作为选择起始行的基础。 这是一种绝对寻址的格式，因为它不依赖于当前游标位置。 要滚动到书签行，应用程序调用**SQLFetchScroll，** 获取*方向*为 SQL_FETCH_BOOKMARK。 此操作使用SQL_ATTR_FETCH_BOOKMARK_PTR语句属性指向的书签。 它将返回以该书签标识的行开始的行集。 应用程序可以在调用**SQLFetchScroll**的*FetchOffset*参数中指定此操作的偏移量。 指定偏移量时，通过将*FetchOffset*参数中的数字添加到书签标识的行数来确定返回的行集的第一行。 与 ODBC 2 一起使用时，不支持使用*FetchOffset*参数。*x*驱动程序;当应用程序在 ODBC 2 中调用**SQLFetchScroll**时。*将**取取方向*设置为SQL_FETCH_BOOKMARK的 x 驱动程序必须将*FetchOffset*参数设置为 0。
