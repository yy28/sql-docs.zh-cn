---
title: 创建索引语句限制 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280878"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 语句限制
Microsoft Excel 或文本驱动程序不支持创建索引语句。  
  
 索引最多可以在 10 列上定义。 如果 CREATE INDEX 语句中包含超过 10 列，则无法识别索引，并且表将被视为未创建索引。  
  
 dBASE 驱动程序无法在"逻辑"列上创建索引。  
  
 使用 dBASE 驱动程序时，可以通过在 SELECT 语句的 WHERE 子句中指定的列（字段）上生成 .mdx（或 .ndx） 索引来提高大型文件的响应时间。 现有 .mdx 索引将自动应用于 WHERE 子句和\<LIKE 谓词中的 *、>、>*、*<和"关系运算符"以及联接谓词。  
  
 使用 dBASE 驱动程序时，由 CREATE UNIQUE INDEX 语句创建的索引实际上非唯一，重复值可以插入到索引列中。 只能将具有相同键值的集中的一条记录添加到索引中。  
  
 使用 Paradox 驱动程序时，必须在表中列的连续子集（包括第一列）上定义唯一索引。 如果在表上未定义唯一索引，或者在没有实现 Borland 数据库引擎的情况下使用 Paradox 驱动程序时，悖论驱动程序无法更新表。
