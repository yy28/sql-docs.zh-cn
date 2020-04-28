---
title: 比较书签 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307472"
---
# <a name="comparing-bookmarks"></a>比较书签
因为书签是字节可比较的，所以可以比较它们是否相等。 为此，应用程序将每个书签视为字节数组，并按字节对两个书签进行比较。 因为仅保证书签在结果集内是唯一的，所以比较从不同结果集中获取的书签没有任何意义。
