---
title: 比较书签 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307472"
---
# <a name="comparing-bookmarks"></a>比较书签
由于书签是字节可比的，因此可以比较它们对于相等或不等式。 为此，应用程序将每个书签视为字节数组，并逐字节比较两个书签字节。 由于书签保证仅在结果集中中不同，因此比较从不同结果集获得的书签是没有意义的。
