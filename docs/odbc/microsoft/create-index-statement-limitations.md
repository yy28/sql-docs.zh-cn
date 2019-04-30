---
title: CREATE INDEX 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec6ba27197f7a6021aff90d30884129128cb3614
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232284"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 语句限制
Microsoft Excel 或文本文件驱动程序不支持 CREATE INDEX 语句。  
  
 可以在最多 10 个列上定义索引。 如果在 CREATE INDEX 语句中包含 10 个以上的列，将不会识别索引和表将被视为与不创建任何索引。  
  
 DBASE 驱动程序不能逻辑列创建索引。  
  
 当使用 dBASE 驱动程序时，可通过在 SELECT 语句的 WHERE 子句中指定的列 （字段） 上构建.mdx （或.ndx） 索引提高大型文件上的响应时间。 现有.mdx 索引将自动应用对于 =，>， \<，> =、 = <，并在 WHERE 子句和 LIKE 谓词，以及联接谓词中运算符之间。  
  
 当使用 dBASE 驱动程序时，CREATE UNIQUE INDEX 语句创建的索引会实际上不唯一，并重复的值可以插入到索引的列。 从具有相同键值的一组只有一条记录可添加到索引。  
  
 当使用 Paradox 驱动程序时，必须在连续中包括的第一列的表的列的子集时定义唯一索引。 如果未对表或 Paradox 驱动程序使用而无需 borland 公司数据库引擎的实现时定义唯一索引，则不能通过 Paradox 驱动程序更新的表。
