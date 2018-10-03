---
title: LIKE 谓词限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8035eed9e0aaff1f914f386b6d4bc9f2d65f9a0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652967"
---
# <a name="like-predicate-limitations"></a>LIKE 谓词限制
如果列中的数据的长度超过 255 个字符，LIKE 比较将基于仅前 255 个字符。  
  
 在中使用一个类似过程仅支持常量模式。 桌面数据库驱动程序支持 SQL-92 等模式匹配。  
  
 不支持使用 LIKE 谓词中的转义子句。  
  
 不应在一列以包含 numeric 或 float 数据类型的数据执行 LIKE 比较。 结果可能不可预测。 有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。
