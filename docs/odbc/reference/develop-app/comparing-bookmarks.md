---
title: 比较书签 |Microsoft 文档
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
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cb844592d47e46a38f431f0127845583b82498a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909372"
---
# <a name="comparing-bookmarks"></a>比较的书签
因为字节比较，书签将变为，它们可以比较相等。 为此，应用程序将视为的字节数组的每个书签，并比较两个书签的字节。 要仅在结果集内非重复，保证具有书签，因为它没有意义要比较的书签，获取从不同的结果集。
