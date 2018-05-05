---
title: 隐式分配描述符 |Microsoft 文档
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
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d805b110453c5fe0bb5be8c8df067c09ff8146e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="implicitly-allocated-descriptors"></a>隐式分配的描述符
分配的语句句柄后，应用程序将隐式分配一组四个描述符。 应用程序可以获得这些隐式分配作为语句句柄的特性的描述符句柄。 当应用程序释放语句句柄时，该驱动程序将释放该句柄上的所有隐式分配的描述符。
