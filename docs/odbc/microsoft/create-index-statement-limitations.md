---
title: 创建索引语句限制 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9501e07fcdb70984153a718eed22be4d5448ec9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32898932"
---
# <a name="create-index-statement-limitations"></a>创建索引语句的限制
Microsoft Excel 或文本驱动程序不支持 CREATE INDEX 语句。  
  
 可以在最多 10 列上定义索引。 如果 10 个以上的列包括在 CREATE INDEX 语句中，将不识别索引和表将其视为好像没有索引创建。  
  
 DBASE 驱动程序无法在逻辑列上创建索引。  
  
 当使用 dBASE 驱动程序时，可以通过生成的列 （域） 的 SELECT 语句的 WHERE 子句中指定.mdx （或.ndx） 索引改进大型文件上的响应时间。 现有.mdx 索引将自动应用于 =，>， \<，> =、 = <，和 BETWEEN 运算符在 WHERE 子句中，和 LIKE 谓词，以及在联接谓词。  
  
 当使用 dBASE 驱动程序时，CREATE UNIQUE INDEX 语句创建的索引是实际是非唯一的并重复的值可以插入到索引的列。 只有一条记录从具有相同键值的一组可以添加到索引。  
  
 当使用 Paradox 驱动程序时，必须时连续中包括的第一列的表的列的子集定义唯一索引。 表不能通过 Paradox 驱动程序更新，如果对表或 Paradox 驱动程序使用不高数据库引擎的实现时，未定义唯一索引。
