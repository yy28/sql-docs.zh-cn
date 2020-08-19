---
description: 比较书签
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
ms.openlocfilehash: 939c3780fc9c6738a307e9a969a346951cfac5e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476779"
---
# <a name="comparing-bookmarks"></a>比较书签
因为书签是字节可比较的，所以可以比较它们是否相等。 为此，应用程序将每个书签视为字节数组，并按字节对两个书签进行比较。 因为仅保证书签在结果集内是唯一的，所以比较从不同结果集中获取的书签没有任何意义。
