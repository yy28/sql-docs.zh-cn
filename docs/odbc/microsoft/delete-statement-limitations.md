---
title: "DELETE 语句限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d8ffdb2fa548b03ee38c0f817675cb88ab4acf67
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="delete-statement-limitations"></a>删除语句的限制
Microsoft Excel 或文本驱动程序不支持 DELETE 语句。 请注意文本驱动程序支持 INSERT 语句。  
  
 DBASE 驱动程序不支持装箱用于删除"删除"的值的表。  
  
 对于从表中删除的行可能是驱动程序，表必须具有唯一索引 （Paradox 主键）。

