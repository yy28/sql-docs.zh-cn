---
title: ALTER TABLE 语句限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1333cd6cd5946b7a3a70152e12f4d3decfa7fed0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138425"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 语句限制
DBASE 或 Paradox 驱动程序使用时，一旦创建索引并添加新记录，ALTER TABLE 语句不能更改表的结构，除非删除索引和表的内容被删除。  
  
 Microsoft Excel 或文本文件驱动程序不支持 ALTER TABLE 语句。  
  
> [!NOTE]  
>  当您使用 Paradox 驱动程序而无需实现 borland 公司数据库引擎时，不支持 ALTER TABLE 语句;仅读取和追加允许使用的语句。
