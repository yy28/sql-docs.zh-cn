---
title: 按书签滚动 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c20c6fd7c9d18e7e1c49f6882d6239749637d7a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913232"
---
# <a name="scrolling-by-bookmark"></a>按书签滚动
在提取的行时**SQLFetchScroll**，应用程序可以将书签用作基础用于选择的起始行。 这是一种绝对寻址的格式，因为它不依赖于当前游标位置。 要滚动到书签的行，则应用程序调用**SQLFetchScroll**与*FetchOrientation* SQL_FETCH_BOOKMARK。 此操作使用的 SQL_ATTR_FETCH_BOOKMARK_PTR 语句属性指向该书签。 它将返回以该书签标识的行开始的行集。 应用程序可以指定在此操作的偏移量*FetchOffset*到调用自变量**SQLFetchScroll**。 当指定偏移量时，由返回的行集的第一行添加中的数字*FetchOffset*自变量由书签的行数。 这种用法*FetchOffset*参数，不支持与 ODBC 2 一起使用时。*x*驱动程序; 当应用程序调用**SQLFetchScroll** ODBC 2 中。*x*驱动程序与*FetchOrientation*设置为 SQL_FETCH_BOOKMARK， *FetchOffset*参数必须设置为 0。
