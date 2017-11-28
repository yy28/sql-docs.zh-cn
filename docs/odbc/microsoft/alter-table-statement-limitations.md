---
title: "ALTER 表语句限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: acdeccfa07141c267a77a927217ad2ec610034c7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="alter-table-statement-limitations"></a>ALTER 表语句的限制
DBASE 或 Paradox 驱动程序使用时，一旦创建索引并添加一条新记录，ALTER TABLE 语句无法更改表的结构，除非删除索引和表的内容被删除。  
  
 为 Microsoft Excel 或文本驱动程序不支持 ALTER TABLE 语句。  
  
> [!NOTE]  
>  当你使用 Paradox 驱动程序而无需实现高数据库引擎时，不支持 ALTER TABLE 语句;仅读取和追加允许语句。
