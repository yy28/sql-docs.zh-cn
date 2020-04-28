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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280878"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 语句限制
Microsoft Excel 或文本驱动程序不支持 CREATE INDEX 语句。  
  
 最多可以定义10个列的索引。 如果 CREATE INDEX 语句中包含10个以上的列，则将不会识别索引，并且该表将被视为未创建索引。  
  
 DBASE 驱动程序无法对逻辑列创建索引。  
  
 使用 dBASE 驱动程序时，可以通过在 SELECT 语句的 WHERE 子句中指定的列（字段）上生成一个或多个 mdx （或 ndx）索引，来改进大型文件的响应时间。 现有的. 将在 WHERE 子句中的 =、>、 \<、>=、=< 和运算符之间自动应用 mdx 索引，并在联接谓词中应用。  
  
 使用 dBASE 驱动程序时，CREATE UNIQUE INDEX 语句创建的索引实际上是不唯一的，并且可以在索引列中插入重复值。 只能将具有相同键值的集中的一条记录添加到索引中。  
  
 使用 Paradox 驱动程序时，必须在表中的列的连续子集上定义唯一索引，包括第一列。 如果表上未定义唯一索引，或在未实现 Borland 数据库引擎的情况下使用 Paradox 驱动程序，则 Paradox 驱动程序无法更新表。
