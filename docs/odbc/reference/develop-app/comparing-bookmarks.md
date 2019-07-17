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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44da652ad1e52934fa48f32b1b2f88b30212ad3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083307"
---
# <a name="comparing-bookmarks"></a>比较书签
因为字节比较，书签将变为，所以可以比较相等。 若要执行此操作，应用程序将视为一个字节数组的每个书签，并比较两个的书签的字节。 要仅在结果集内非重复，保证具有书签，因为它没有意义比较来自不同的结果集获得的书签。
