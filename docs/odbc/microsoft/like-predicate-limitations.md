---
title: 喜欢谓词限制 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d596d688956d7bdbf3d9125184d81c16249781c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298957"
---
# <a name="like-predicate-limitations"></a>LIKE 谓词限制
如果列中的数据长于 255 个字符，则 LIKE 比较将仅基于前 255 个字符。  
  
 过程中使用的 LIKE 仅支持常量模式。 桌面数据库驱动程序支持 SQL-92 LIKE 模式匹配。  
  
 不支持在 LIKE 谓词中使用转义子句。  
  
 不应在包含数字或浮点数据类型数据的列上执行类似数据比较。 结果可能是不可预测的。 有关详细信息，请参阅 Microsoft*喷气数据库引擎程序员指南*。
