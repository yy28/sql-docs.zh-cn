---
title: ORDER BY 子句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ORDER BY clause limitations
- ORDER BY clause limitations [ODBC]
ms.assetid: fd4ddc7c-9c7e-4a0c-a781-e5427dfb2e18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2835396a7b8266d812ca5a1049679c7d82549389
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63024348"
---
# <a name="order-by-clause-limitations"></a>ORDER BY 子句限制
如果 SELECT 语句包含 GROUP BY 子句和 ORDER BY 子句，仅在结果集中的列或 GROUP BY 子句中的表达式可以包含 ORDER BY 子句。
