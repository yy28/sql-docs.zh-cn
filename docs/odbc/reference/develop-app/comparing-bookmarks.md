---
title: "比较书签 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12eb00507a60fac6b49e0d8f9a5c8a5a3d3a32cf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="comparing-bookmarks"></a>比较的书签
因为字节比较，书签将变为，它们可以比较相等。 为此，应用程序将视为的字节数组的每个书签，并比较两个书签的字节。 要仅在结果集内非重复，保证具有书签，因为它没有意义要比较的书签，获取从不同的结果集。
