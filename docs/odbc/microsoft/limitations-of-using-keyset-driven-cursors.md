---
title: 使用由键集驱动的游标的限制 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284147"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用由键集驱动的游标的限制
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 您必须能够检索所查询的表的单个 ROWID 列。 由键集驱动的游标不能用于包含 DISTINCT、GROUP BY、UNION、INTERSECT 或减法子句的联接、查询或语句。  
  
 此外，如果应用程序使用表别名，则键集驱动游标将不起作用;需要只进或静态游标类型。 在表别名中使用键集游标类型将导致以下错误： "[Microsoft] [ODBC driver for Oracle] 无法在联接时使用 union、intersect 或减号或只读结果集上的键集驱动游标。"  
  
> [!NOTE]  
>  由于驱动程序处理发送到 Oracle 服务器的 SQL 语句的方式，Oracle 内部返回以下错误消息： "TNSNAMES.ORA-00964：表名称不在列表中"。
