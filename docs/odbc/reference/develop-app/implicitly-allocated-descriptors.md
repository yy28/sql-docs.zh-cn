---
title: 隐式分配的描述符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 271d479a9d2faa8cd7ab01e02e830b194c4138b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300127"
---
# <a name="implicitly-allocated-descriptors"></a>隐式分配的描述符
分配语句句柄时，应用程序隐式分配一组四个描述符。 应用程序可以获取这些隐式分配的描述符的句柄作为语句句柄的属性。 当应用程序释放语句句柄时，驱动程序将释放该句柄上所有隐式分配的描述符。
