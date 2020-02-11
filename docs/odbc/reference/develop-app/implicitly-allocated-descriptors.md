---
title: 隐式分配的描述符 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138945"
---
# <a name="implicitly-allocated-descriptors"></a>隐式分配的描述符
当分配语句句柄时，应用程序会隐式分配一组四个说明符。 应用程序可以获取这些隐式分配的描述符的句柄作为语句句柄的特性。 当应用程序释放语句句柄时，驱动程序将释放该句柄上的所有隐式分配的说明符。
