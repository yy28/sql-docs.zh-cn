---
title: 检索书签 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300067"
---
# <a name="retrieving-bookmarks"></a>检索书签
如果应用程序将使用书签，则必须在准备或执行语句之前将SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE。 这是必需的，因为构建和维护书签可能是一项昂贵的操作，因此只有在应用程序能够很好地使用它们时才能启用书签。  
  
 书签将作为结果集的第 0 列返回。 应用程序可以检索它们的方法有三种：  
  
-   绑定结果集的列 0。 **SQLFetch**或**SQLFetchScroll**返回行集中每行的书签以及其他绑定列的数据。  
  
-   调用**SQLSetPos**定位到行集中的行，然后为列 0 调用**SQLGetData。** 如果驱动程序支持书签，它必须始终支持为列 0 调用**SQLGetData**的能力，即使它不允许应用程序在最后一个绑定列之前为其他列调用**SQLGetData。**  
  
-   调用**SQLBulk 操作**，*操作*参数设置为SQL_ADD，第 0 列绑定。 光标插入该行并返回绑定缓冲区中行的书签。
