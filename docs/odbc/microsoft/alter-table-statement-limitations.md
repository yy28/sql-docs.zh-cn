---
title: 更改表语句限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304696"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 语句限制
使用 dBASE 或 Paradox 驱动程序时，创建索引并添加新记录后，ALTER TABLE 语句无法更改表的结构，除非删除索引并删除表的内容。  
  
 Microsoft Excel 或文本驱动程序不支持 ALTER TABLE 语句。  
  
> [!NOTE]  
>  当您在不实现 Borland 数据库引擎的情况下使用 Paradox 驱动程序时，不支持 ALTER TABLE 语句;因此，如果不执行"不带悖论"，则不支持 ALTER TABLE 语句。仅允许读取和追加语句。
