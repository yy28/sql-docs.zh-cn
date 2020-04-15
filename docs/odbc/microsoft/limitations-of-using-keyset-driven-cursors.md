---
title: 使用键集驱动光标的限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aeb5a0c50192118dfff8ed7d866c3911c2b4007
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284147"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用由键集驱动的游标的限制
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 您必须能够检索查询的表的单个 ROWID 列。 键集驱动的游标不能用于包含"差异"、组 BY、UNION、INTERSECT 或 MINUS 子句的联接、查询或语句。  
  
 此外，如果应用程序使用表别名，则键集驱动的游标将不起作用;如果应用程序使用表别名，则键集驱动的游标将不起作用。需要仅转发或静态游标类型。 使用带有表别名的键集游标类型将导致以下错误："[Microsoft][Oracle 的 ODBC 驱动程序]无法在联接、联合、相交或减或只读结果集上使用 Keyset 驱动的游标。  
  
> [!NOTE]  
>  由于驱动程序处理发送到 Oracle 服务器的 SQL 语句的方式，Oracle 内部返回以下错误消息："ORA-00964：表名不在 FROM 列表中。
