---
title: 按书签滚动 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90ba6ed3a6feb163fbe1eaf39cce14ae501c232e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468373"
---
# <a name="scrolling-by-bookmark"></a>按书签滚动
提取的行时**SQLFetchScroll**，应用程序可以用于选择开始行作为基础使用书签。 这是一种绝对寻址的格式，因为它不依赖于当前游标位置。 若要滚动到带书签的行，应用程序调用**SQLFetchScroll**与*FetchOrientation*的 SQL_FETCH_BOOKMARK。 此操作使用 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性所指向的书签。 它将返回以该书签标识的行开始的行集。 应用程序可以指定在此操作的偏移量*FetchOffset*的调用的参数**SQLFetchScroll**。 如果指定偏移量，则由返回的行集的第一行添加中的数字*FetchOffset*参数由书签标识的行数。 这种用法*FetchOffset*与 ODBC 2 一起使用时，不支持参数。*x*驱动程序; 当应用程序调用**SQLFetchScroll** ODBC 2 中。*x*驱动程序与*FetchOrientation*设置为 SQL_FETCH_BOOKMARK， *FetchOffset*参数必须设置为 0。
