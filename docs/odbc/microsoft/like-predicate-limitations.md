---
title: 如谓词限制 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73e4ec1b4177b02869939628cb408df500958694
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="like-predicate-limitations"></a>如谓词限制
如果列中的数据的长度超过 255 个字符，如比较将基于仅前 255 个字符。  
  
 在中使用 LIKE 过程支持仅具有常量模式。 桌面数据库驱动程序支持 SQL 92 如模式匹配。  
  
 不支持使用 LIKE 谓词中的转义子句。  
  
 不应在一列以包含数字或 float 数据类型的数据执行 LIKE 比较。 结果可能会产生不可预知。 有关详细信息，请参阅*Microsoft Jet 数据库引擎程序员指南*。
