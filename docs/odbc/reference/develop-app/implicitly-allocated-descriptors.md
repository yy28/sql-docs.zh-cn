---
title: 隐式分配描述符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0eb34866b75802a32c63e62b41d384e5a1dea73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138945"
---
# <a name="implicitly-allocated-descriptors"></a>隐式分配的描述符
分配语句句柄后，应用程序将隐式分配一组四个描述符。 应用程序可以获取这些隐式分配语句句柄的属性描述符句柄。 当应用程序释放语句句柄时，该驱动程序将释放该句柄上的所有隐式分配的描述符。
