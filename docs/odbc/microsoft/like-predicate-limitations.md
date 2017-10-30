---
title: "如谓词限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5668f03e785c0d27133965f16af40ce69c2a2567
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="like-predicate-limitations"></a>如谓词限制
如果列中的数据的长度超过 255 个字符，如比较将基于仅前 255 个字符。  
  
 在中使用 LIKE 过程支持仅具有常量模式。 桌面数据库驱动程序支持 SQL 92 如模式匹配。  
  
 不支持使用 LIKE 谓词中的转义子句。  
  
 不应在一列以包含数字或 float 数据类型的数据执行 LIKE 比较。 结果可能会产生不可预知。 有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。

