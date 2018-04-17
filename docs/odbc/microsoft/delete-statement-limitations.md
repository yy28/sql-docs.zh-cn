---
title: DELETE 语句限制 |Microsoft 文档
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
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45386d8278e968b55fba5881dfe9b914bc23f454
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="delete-statement-limitations"></a>删除语句的限制
Microsoft Excel 或文本驱动程序不支持 DELETE 语句。 请注意文本驱动程序支持 INSERT 语句。  
  
 DBASE 驱动程序不支持装箱用于删除"删除"的值的表。  
  
 对于从表中删除的行可能是驱动程序，表必须具有唯一索引 （Paradox 主键）。
