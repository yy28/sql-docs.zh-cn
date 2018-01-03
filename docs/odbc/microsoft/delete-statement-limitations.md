---
title: "DELETE 语句限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cce6402f913348dd3b9aa3d116b7ceffb5a55ea4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="delete-statement-limitations"></a>删除语句的限制
Microsoft Excel 或文本驱动程序不支持 DELETE 语句。 请注意文本驱动程序支持 INSERT 语句。  
  
 DBASE 驱动程序不支持装箱用于删除"删除"的值的表。  
  
 对于从表中删除的行可能是驱动程序，表必须具有唯一索引 （Paradox 主键）。
